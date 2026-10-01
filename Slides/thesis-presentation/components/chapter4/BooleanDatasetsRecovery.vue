<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)
let chart = null
let resizeObserver = null

const timeSteps = ['10', '20', '30', '40', '50', '60', '70', '80', '90']

const origin = {
  1: [
    {
      precision: [0.376663, 0.449354, 0.524465, 0.578733, 0.605513, 0.615241, 0.627472, 0.643735, 0.637062],
      recall: [0.249095, 0.440879, 0.540288, 0.590682, 0.616961, 0.617420, 0.625843, 0.639646, 0.637786],
      structural: [0.946571, 0.949592, 0.956367, 0.961510, 0.963837, 0.964531, 0.965510, 0.966816, 0.966286],
      dynamics: [0.997333, 0.997684, 0.990759, 0.990051, 0.989469, 0.991119, 0.991884, 0.993823, 0.993753]
    },
    {
      precision: [0.08893069, 0.04274188, 0.07147663, 0.06728597, 0.08278309, 0.09301868, 0.10133796, 0.12573227, 0.12632815],
      recall: [0.05807883, 0.04401191, 0.07000260, 0.07101441, 0.07756933, 0.09025530, 0.09033250, 0.11356950, 0.11311673],
      structural: [0.00753158, 0.00547989, 0.00738189, 0.00685192, 0.00846228, 0.00965796, 0.01019142, 0.01251412, 0.01264147],
      dynamics: [0.00294811, 0.00332205, 0.00302506, 0.00378377, 0.00539579, 0.00507751, 0.00337031, 0.00309483, 0.00299779]
    }
  ],

  2: [
    {
      precision: [0.314316, 0.409347, 0.470623, 0.496885, 0.561176, 0.588044, 0.613380, 0.626186, 0.643329],
      recall: [0.187459, 0.376571, 0.490034, 0.526851, 0.584967, 0.607279, 0.625330, 0.634937, 0.647730],
      structural: [0.972172, 0.973414, 0.975737, 0.976939, 0.980040, 0.981263, 0.982495, 0.983051, 0.983848],
      dynamics: [0.996222, 0.999158, 0.994828, 0.988667, 0.987837, 0.988339, 0.989420, 0.989873, 0.991348]
    },
    {
      precision: [0.05403114, 0.02986717, 0.04682752, 0.04085743, 0.05010288, 0.05604578, 0.04764701, 0.05218377, 0.05758091],
      recall: [0.02899745, 0.02248577, 0.04057775, 0.02905347, 0.05145557, 0.05220270, 0.05571477, 0.06071238, 0.07015162],
      structural: [0.00248873, 0.00225223, 0.00313418, 0.00293244, 0.00313984, 0.00321182, 0.00254980, 0.00278422, 0.00288665],
      dynamics: [0.00298969, 0.00122757, 0.00205165, 0.00388832, 0.00503151, 0.00615084, 0.00471003, 0.00458920, 0.00412315]
    }
  ]
}

const synthetic = {
  1: [
    {
      precision: [0.381909, 0.467466, 0.538150, 0.584155, 0.606819, 0.630231, 0.631593, 0.643044, 0.643184],
      recall: [0.336956, 0.475394, 0.572924, 0.620661, 0.645242, 0.645058, 0.646515, 0.647953, 0.645438],
      structural: [0.954776, 0.957429, 0.961143, 0.965857, 0.967102, 0.966388, 0.969061, 0.967837, 0.967531],
      dynamics: [0.999596, 0.999394, 0.995354, 0.989859, 0.988525, 0.989758, 0.990909, 0.989333, 0.989778]
    }
  ],

  2: [
    {
      precision: [0.381053, 0.429104, 0.485143, 0.534663, 0.593444, 0.611028, 0.637700, 0.641917, 0.647177],
      recall: [0.227822, 0.377374, 0.495327, 0.557610, 0.621048, 0.636483, 0.647019, 0.648757, 0.649230],
      structural: [0.979818, 0.981101, 0.982990, 0.982768, 0.984339, 0.984566, 0.984570, 0.984677, 0.985192],
      dynamics: [0.998727, 0.998263, 0.992980, 0.987879, 0.985899, 0.980162, 0.981980, 0.982788, 0.983899]
    }
  ]
}

const metrics = [
  { key: 'precision', name: 'Precision', color: '#40E0D0' },
  { key: 'recall', name: 'Recall', color: '#FF7F50' },
  { key: 'structural', name: 'Structural', color: '#000000' }
]

/* subplot letters, row0 = a,b,c / row1 = d,e,f */
const letters = ['a', 'b', 'c', 'd', 'e', 'f']

const findings = [
  { number: '01', title: 'Broad Effectiveness', text: 'Precision, recall, and structural accuracy improvements confirmed on binary Boolean networks.' },
  { number: '02', title: 'Scale-Dependent Trends', text: 'For N=50, recall gains were larger on average. For N=100, precision gains were larger on average.' },
  { number: '03', title: 'Zero Negative Impact', text: 'Adding synthetic gene expression data caused no performance degradation in any scenario.' }
]

function improvement(network, metric) {
  return synthetic[network][0][metric].map((v, i) => v - origin[network][0][metric][i])
}

/* =========================================================
   PRIMARY AXIS SERIES (Synthetic solid / Origin dashed)
   Names are encoded as "label|role|axis" so a per-chart
   legend can show just the metric name while the tooltip
   can still tell synthetic apart from origin.
   ========================================================= */

function lineSeries(data, color, name, axis, dashed = false) {
  return {
    type: 'line',
    name,
    xAxisIndex: axis,
    yAxisIndex: axis,
    data,
    smooth: false,
    symbol: 'circle',
    symbolSize: 7,
    showSymbol: true,
    z: 5,
    lineStyle: { color, width: 2.5, type: dashed ? 'dashed' : 'solid' },
    itemStyle: { color, borderColor: '#24313A', borderWidth: 1.2 }
  }
}

/* =========================================================
   TWIN AXIS SERIES (Improvement bars)
   ========================================================= */

function barSeries(data, axis, name) {
  return {
    type: 'bar',
    name,
    xAxisIndex: axis,
    yAxisIndex: axis + 6,
    data,
    barWidth: 13,
    z: 1,
    itemStyle: { color: '#2E86C1', opacity: 0.8 }
  }
}

function errorSeries(means, stds, axis) {
  return {
    type: 'custom',
    name: 'Error',
    xAxisIndex: axis,
    yAxisIndex: axis,
    silent: true,
    z: 6,
    renderItem(params, api) {
      const index = params.dataIndex
      const mean = api.value(1)
      const std = api.value(2)
      const point = api.coord([index, mean])
      const upper = api.coord([index, mean + std])
      const lower = api.coord([index, mean - std])
      const cap = 3
      return {
        type: 'group',
        children: [
          { type: 'line', shape: { x1: point[0], y1: upper[1], x2: point[0], y2: lower[1] }, style: { stroke: '#d72626', lineWidth: 1.4 } },
          { type: 'line', shape: { x1: point[0] - cap, y1: upper[1], x2: point[0] + cap, y2: upper[1] }, style: { stroke: '#d72626', lineWidth: 1.4 } },
          { type: 'line', shape: { x1: point[0] - cap, y1: lower[1], x2: point[0] + cap, y2: lower[1] }, style: { stroke: '#d72626', lineWidth: 1.4 } }
        ]
      }
    },
    data: means.map((value, i) => [i, value, stds[i]])
  }
}

function twinRange(row, col) {
  if (col === 2) return { min: -0.01, max: 0.3 }
  return row === 0 ? { min: -0.01, max: 0.3 } : { min: 0, max: 0.3 }
}

/* legend text: strip the "|role|axis" suffix, keep only the label */
function legendLabelFormatter(name) {
  return name.split('|')[0]
}

function buildOption() {
  const grids = [], xAxes = [], yAxes = [], twinYAxes = [], series = [], legends = []

  const colLeft = ['1.5%', '34.25%', '67%']
  const legendLeft = ['2%', '35%', '68%']

  for (let row = 0; row < 2; row++) {
    for (let col = 0; col < 3; col++) {
      const axis = row * 3 + col
      const letter = letters[axis]
      const isBottomRow = row === 1
      const metric = metrics[col]
      const network = row + 1

      /* unique, role-tagged series names so each subplot's
         legend can control only its own two series */
      const synthName = `${metric.name}|s|${axis}`
      const originName = `${metric.name}|o|${axis}`
      const improvementName = `Improvement|b|${axis}`

      grids.push({
        left: colLeft[col],
        top: row === 0 ? '9%' : '55%',
        width: '31%',
        height: '32%',
        containLabel: true,
        show: true,
        backgroundColor: '#F7F7F7',
        borderWidth: 0
      })

      /* per-subplot legend, floating just above its grid */
      legends.push({
        top: row === 0 ? '1%' : '47%',
        left: legendLeft[col],
        orient: 'horizontal',
        itemWidth: 14,
        itemHeight: 8,
        itemGap: 8,
        backgroundColor: 'rgba(255,255,255,0.85)',
        borderRadius: 3,
        padding: [2, 6],
        textStyle: { fontSize: 8.5, color: '#24313A' },
        formatter: legendLabelFormatter,
        data: [synthName, improvementName]
      })

      xAxes.push({
        type: 'category',
        gridIndex: axis,
        data: timeSteps,
        boundaryGap: true,
        axisLine: { lineStyle: { color: '#000000', width: 1.5 } },
        axisTick: { show: true, length: 5, lineStyle: { color: '#000000', width: 1.2 } },
        axisLabel: { fontSize: 9, color: '#24313A', margin: 6 },
        splitLine: { show: true, lineStyle: { color: '#DDDDDD', type: 'dashed', opacity: 0.6 } },
        name: isBottomRow
          ? `Observed time step number (k)\n(${letter})`
          : `(${letter})`,
        nameLocation: 'middle',
        nameGap: isBottomRow ? 32 : 22,
        nameTextStyle: { fontSize: 10, color: '#24313A', fontWeight: 600, lineHeight: 14 }
      })

      /* primary accuracy axis (0 – 1) */
      yAxes.push({
        type: 'value',
        gridIndex: axis,
        min: 0,
        max: 1,
        interval: 0.2,
        axisLine: { show: col === 0, lineStyle: { color: '#000000', width: 1.5 } },
        axisTick: { show: col === 0, length: 4, lineStyle: { color: '#000000', width: 1.2 } },
        axisLabel: { show: col === 0, fontSize: 9, color: '#24313A', formatter: value => value.toFixed(1) },
        splitLine: { show: true, lineStyle: { color: '#DDDDDD', type: 'dashed', opacity: 0.6 } },
        name: col === 0 ? 'Accuracy' : '',
        nameLocation: 'middle',
        nameGap: 32,
        nameRotate: 90,
        nameTextStyle: { fontSize: 10, color: '#24313A', fontWeight: 600 },
        z: 3
      })

      /* twin axis for the improvement bars */
      const range = twinRange(row, col)
      twinYAxes.push({
        type: 'value',
        gridIndex: axis,
        min: range.min,
        max: range.max,
        position: 'right',
        axisLine: { show: false },
        axisTick: { show: false },
        splitLine: { show: false },
        axisLabel: {
          show: col === 2,
          fontSize: 9,
          color: '#475569',
          formatter: value => value.toFixed(2)
        },
        name: col === 2 ? 'Improvement rate' : '',
        nameLocation: 'middle',
        nameGap: 34,
        nameTextStyle: { fontSize: 9, color: '#475569' },
        z: 1
      })

      const syntheticMean = synthetic[network][0][metric.key]
      const originMean = origin[network][0][metric.key]
      const originStd = origin[network][1][metric.key]

      series.push(
        barSeries(improvement(network, metric.key), axis, improvementName),
        lineSeries(syntheticMean, metric.color, synthName, axis),
        lineSeries(originMean, metric.color, originName, axis, true),
        errorSeries(originMean, originStd, axis)
      )
    }
  }

  return {
    animationDuration: 600,
    legend: legends,
    grid: grids,
    xAxis: xAxes,
    yAxis: [...yAxes, ...twinYAxes],
    tooltip: {
      trigger: 'axis',
      confine: true,
      formatter(params) {
        if (!params.length) return ''
        const k = timeSteps[params[0].dataIndex]
        let synthetic, original, improvementValue
        params.forEach(p => {
          if (p.seriesName.includes('|s|')) synthetic = p.value
          else if (p.seriesName.includes('|o|')) original = p.value
          else if (p.seriesName.includes('|b|')) improvementValue = p.value
        })
        return `<strong>K = ${k}</strong><br/>${synthetic !== undefined ? '● Synthetic: ' + Number(synthetic).toFixed(3) + '<br/>' : ''}${original !== undefined ? '● Original: ' + Number(original).toFixed(3) + '<br/>' : ''}${improvementValue !== undefined ? '■ Improvement: ' + Number(improvementValue).toFixed(3) : ''}`
      }
    },
    series
  }
}

function renderChart() {
  if (!chartRef.value) return
  if (chart) chart.dispose()

  chart = echarts.init(chartRef.value, null, {
    renderer: 'svg'
  })

  chart.setOption(buildOption())

  resizeObserver = new ResizeObserver(() => chart?.resize())
  resizeObserver.observe(chartRef.value)
}

onMounted(async () => {
  await nextTick()
  renderChart()
})

onBeforeUnmount(() => {
  resizeObserver?.disconnect()
  if (chart) {
    chart.dispose()
    chart = null
  }
})
</script>

<template>
  <div class="recovery-slide">
    <div ref="chartRef" class="recovery-chart"></div>
    <div class="findings">
      <div v-for="item in findings" :key="item.number" class="finding">
        <div class="finding-header"><span class="finding-number">{{ item.number }}</span><h3>{{ item.title }}</h3></div>
        <p>{{ item.text }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.recovery-slide { width:100%; height:100%; box-sizing:border-box; display:flex; flex-direction:column; overflow:auto; }
.recovery-chart { width:100%; height:80%; min-height:0; }
.findings { width:100%; display:grid; grid-template-columns:repeat(3,1fr); gap:10px; margin-top:15px; }
.finding { min-width: 0; box-sizing: border-box; padding: 7px 9px; border-top: 2px solid #b3cedf; background: #fff; position: relative; z-index: 1; transition: transform 0.22s ease, box-shadow 0.22s ease, border-top-color 0.22s ease; } /* * Lift effect when hovering */ 
.finding:hover { transform: translateY(-4px); border-top-color: #2A9D8F; box-shadow: 0 7px 16px rgba(23, 63, 95, 0.12), 0 2px 5px rgba(23, 63, 95, 0.06); z-index: 5; }
.finding:hover .finding-number { transform: scale(1.08); color: #20639B; }
.finding:hover h3 { color: #20639B; }
.finding-header { display:flex; align-items:baseline; gap:6px; margin-bottom:3px; }
.finding-number { flex:0 0 auto; color:#2A9D8F; font-family:'IBM Plex Mono','JetBrains Mono',monospace; font-size:9.5px; font-weight:700; letter-spacing:.08em; }
.finding h3 { margin:0; color:#173F5F; font-size:10.5px; line-height:1.2; font-weight:700; }
.finding p { margin:0; color:#64748B; font-size:9px; line-height:1.28; }
@media (max-width:1000px) { .findings { grid-template-columns:repeat(2,1fr); } .recovery-chart { height:70%; } }
</style>