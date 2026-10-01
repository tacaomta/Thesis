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
      precision: [0.298477, 0.468009, 0.569317, 0.636600, 0.685963, 0.728349, 0.744076, 0.767561, 0.782548],
      recall: [0.223638, 0.463881, 0.617590, 0.705546, 0.758981, 0.796875, 0.807769, 0.828885, 0.845271],
      structural: [0.939633, 0.950490, 0.960327, 0.967061, 0.972204, 0.976694, 0.978122, 0.980245, 0.981755],
      dynamics: [0.996889, 0.999368, 0.997448, 0.995026, 0.995102, 0.990712, 0.989072, 0.986987, 0.987843]
    },
    {
      precision: [0.05418565, 0.06904943, 0.06831842, 0.08985879, 0.08496144, 0.08404063, 0.07701596, 0.08417950, 0.08724304],
      recall: [0.04530680, 0.06896370, 0.06989779, 0.07686308, 0.06455024, 0.06933169, 0.06308935, 0.06175157, 0.07189224],
      structural: [0.00612639, 0.00813475, 0.00838038, 0.01024815, 0.00868813, 0.00768703, 0.00703700, 0.00755973, 0.00813679],
      dynamics: [0.00488889, 0.00134803, 0.00506838, 0.00947830, 0.00837879, 0.01145662, 0.00901915, 0.00897517, 0.00699266]
    }
  ],
  2: [
    {
      precision: [0.215274, 0.415903, 0.502496, 0.587460, 0.627109, 0.674407, 0.701331, 0.723899, 0.728534],
      recall: [0.160646, 0.406729, 0.557086, 0.670740, 0.728845, 0.773813, 0.797327, 0.813784, 0.813580],
      structural: [0.967242, 0.973172, 0.976990, 0.981475, 0.983626, 0.986101, 0.987414, 0.988404, 0.988535],
      dynamics: [0.998889, 0.999579, 0.999483, 0.998333, 0.992633, 0.987559, 0.983348, 0.981899, 0.978573]
    },
    {
      precision: [0.02927598, 0.05396575, 0.06388454, 0.05372550, 0.06035070, 0.04609257, 0.05341903, 0.07663200, 0.08362757],
      recall: [0.02360571, 0.05217971, 0.06254445, 0.04951558, 0.05476015, 0.04148086, 0.04306689, 0.05909485, 0.06388094],
      structural: [0.00192982, 0.00312257, 0.00401756, 0.00332543, 0.00368249, 0.00269688, 0.00284490, 0.00388247, 0.00421498],
      dynamics: [0.00149071, 0.00051568, 0.00046902, 0.00167061, 0.00833366, 0.01051044, 0.01272418, 0.01236768, 0.01360266]
    }
  ]
}

const synthetic = {
  1: [
    {
      precision: [0.396695, 0.521422, 0.585718, 0.649742, 0.689488, 0.724627, 0.772248, 0.779483, 0.787846],
      recall: [0.417649, 0.532498, 0.638485, 0.718701, 0.759960, 0.788405, 0.818261, 0.831362, 0.846195],
      structural: [0.957224, 0.953714, 0.964551, 0.974469, 0.972388, 0.976102, 0.980245, 0.981469, 0.981102],
      dynamics: [0.999394, 0.999374, 0.997354, 0.995434, 0.989879, 0.984626, 0.984061, 0.979495, 0.984889]
    }
  ],
  2: [
    {
      precision: [0.285548, 0.425758, 0.564899, 0.599179, 0.641044, 0.685386, 0.707371, 0.731094, 0.740657],
      recall: [0.395047, 0.475931, 0.571188, 0.698556, 0.728961, 0.798055, 0.817280, 0.818566, 0.823367],
      structural: [0.981020, 0.975515, 0.979283, 0.983899, 0.981929, 0.987596, 0.985384, 0.986636, 0.983424],
      dynamics: [0.999636, 0.997778, 0.998444, 0.991030, 0.979758, 0.977141, 0.968889, 0.969667, 0.972010]
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
  { number: '01', title: 'Consistent Improvement', text: 'Synthetic data consistently increases precision and recall across almost all observed time steps (K).' },
  { number: '02', title: 'Maximum Impact at Low K', text: 'The largest gains occur when real observations are scarcest, especially at K = 10 and K = 20.' },
  { number: '03', title: 'Scalability', text: 'Similar performance gains are observed for both N = 50 and N = 100 gene-scale networks.' },
  { number: '04', title: 'Structural Accuracy Stability', text: 'Structural accuracy changes only slightly because of the large true-negative baseline.' }
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
.findings { width:100%; display:grid; grid-template-columns:repeat(4,1fr); gap:10px; margin-top:15px; }
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