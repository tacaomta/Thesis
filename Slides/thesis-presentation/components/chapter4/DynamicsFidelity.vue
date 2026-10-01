<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)
let chart = null
let resizeObserver = null

/* =========================================================
   DATA
   ========================================================= */

const ternaryOrigin = {
  1: { dynamics: [0.996889, 0.999368, 0.997448, 0.995026, 0.995102, 0.990712, 0.989072, 0.986987, 0.987843] },
  2: { dynamics: [0.998889, 0.999579, 0.999483, 0.998333, 0.992633, 0.987559, 0.983348, 0.981899, 0.978573] }
}

const ternarySynthetic = {
  1: { dynamics: [0.999394, 0.999374, 0.997354, 0.995434, 0.989879, 0.984626, 0.984061, 0.979495, 0.984889] },
  2: { dynamics: [0.999636, 0.997778, 0.998444, 0.991030, 0.979758, 0.977141, 0.968889, 0.969667, 0.972010] }
}

const booleanOrigin = {
  1: { dynamics: [0.997333, 0.997684, 0.990759, 0.990051, 0.989469, 0.991119, 0.991884, 0.993823, 0.993753] },
  2: { dynamics: [0.996222, 0.999158, 0.994828, 0.988667, 0.987837, 0.988339, 0.989420, 0.989873, 0.991348] }
}

const booleanSynthetic = {
  1: { dynamics: [0.999596, 0.999394, 0.995354, 0.989859, 0.988525, 0.989758, 0.990909, 0.989333, 0.989778] },
  2: { dynamics: [0.998727, 0.998263, 0.992980, 0.987879, 0.985899, 0.980162, 0.981980, 0.982788, 0.983899] }
}

const xLabels = ['10', '20', '30', '40', '50', '60', '70', '80', '90']

/* row0 = N=50, row1 = N=100 / col0 = Ternary, col1 = Boolean */
const datasets = [
  { type: 'Ternary', network: 'N = 50', origin: ternaryOrigin[1].dynamics, synthetic: ternarySynthetic[1].dynamics },
  { type: 'Boolean', network: 'N = 50', origin: booleanOrigin[1].dynamics, synthetic: booleanSynthetic[1].dynamics },
  { type: 'Ternary', network: 'N = 100', origin: ternaryOrigin[2].dynamics, synthetic: ternarySynthetic[2].dynamics },
  { type: 'Boolean', network: 'N = 100', origin: booleanOrigin[2].dynamics, synthetic: booleanSynthetic[2].dynamics }
]

const findings = [
  { number: '01', title: 'High Baseline Accuracy', text: 'Dynamics accuracy stays above 0.95 across all time steps, for both Ternary and Boolean regimes.' },
  { number: '02', title: 'Minimal Synthetic Drift', text: 'Synthetic-augmented curves track the original closely, with only marginal divergence at higher K.' },
  { number: '03', title: 'Boolean More Stable', text: 'Boolean networks show a narrower accuracy band (0.97–1.10) than Ternary (0.95–1.10).' },
  { number: '04', title: 'Scale-Invariant Behavior', text: 'The pattern holds consistently at both N = 50 and N = 100 gene-scale networks.' }
]

/* =========================================================
   OPTION BUILDER
   ========================================================= */

function buildOption() {
  const grids = []
  const xAxes = []
  const yAxes = []
  const series = []

  /* 2 columns x 2 rows */
  const colLeft = ['8%', '54%']
  const colWidth = '38%'
  const rowTop = ['12%', '58%']
  const rowHeight = '34%'

  datasets.forEach((dataset, index) => {
    const row = Math.floor(index / 2)
    const col = index % 2
    const isTernary = dataset.type === 'Ternary'
    const isBottomRow = row === 1
    const isLeftCol = col === 0

    /* Locked Y-axis range, per requirement:
       Ternary: 0.95 -> 1.10 | Boolean: 0.97 -> 1.10 */
    const yMin = isTernary ? 0.95 : 0.95
    const yMax = 1.00

    grids.push({
      left: colLeft[col],
      top: rowTop[row],
      width: colWidth,
      height: rowHeight,
      containLabel: true,
      show: true,
      backgroundColor: '#FAFAFA',
      borderWidth: 0
    })

    /* per-subplot title (type + network) */
    grids[index].tooltip = undefined

    xAxes.push({
      type: 'category',
      gridIndex: index,
      data: xLabels,
      boundaryGap: false,

      name: isBottomRow ? 'Observed time step number (k)' : '',
      nameLocation: 'middle',
      nameGap: 30,
      nameTextStyle: { fontSize: 10, color: '#000', fontWeight: 600 },

      axisLine: { show: true, lineStyle: { color: '#000', width: 1.5 } },
      axisTick: { show: true, alignWithLabel: true, length: 5, lineStyle: { color: '#000', width: 1.2 } },
      axisLabel: { show: true, color: '#000', fontSize: 9, margin: 6 },
      splitLine: { show: false }
    })

    yAxes.push({
      type: 'value',
      gridIndex: index,

      min: yMin,
      max: yMax,
      interval: 0.05,
      scale: false,

      name: isLeftCol ? 'Accuracy' : '',
      nameLocation: 'middle',
      nameGap: 34,
      nameRotate: 90,
      nameTextStyle: { fontSize: 10, color: '#000', fontWeight: 600 },

      axisLine: { show: true, lineStyle: { color: '#000', width: 1.5 } },
      axisTick: { show: true, length: 5, lineStyle: { color: '#000', width: 1.2 } },
      axisLabel: {
        show: true,
        color: '#000',
        fontSize: 9,
        margin: 6,
        formatter: value => Number(value).toFixed(2)
      },
      splitLine: { show: true, lineStyle: { color: '#B8B8B8', type: 'dashed', width: 0.8 } },
      axisPointer: { show: false }
    })

    series.push(
      {
        name: 'Synthetic',
        type: 'line',
        xAxisIndex: index,
        yAxisIndex: index,
        data: dataset.synthetic,
        clip: true,
        showSymbol: true,
        symbol: 'circle',
        symbolSize: 6,
        z: 5,
        lineStyle: { color: '#425DF5', width: 2.2, type: 'solid' },
        itemStyle: { color: '#425DF5', borderColor: '#000', borderWidth: 1 },
        emphasis: { focus: 'series' }
      },
      {
        name: 'Original',
        type: 'line',
        xAxisIndex: index,
        yAxisIndex: index,
        data: dataset.origin,
        clip: true,
        showSymbol: true,
        symbol: 'circle',
        symbolSize: 6,
        z: 5,
        lineStyle: { color: '#FF7F50', width: 2.2, type: 'dashed' },
        itemStyle: { color: '#FF7F50', borderColor: '#000', borderWidth: 1 },
        emphasis: { focus: 'series' }
      }
    )
  })

  return {
    animation: false,

    /* single shared legend since Synthetic/Original share the
       same 2 colors across all 4 subplots */
    legend: {
      top: 2,
      left: 'center',
      itemWidth: 16,
      itemHeight: 9,
      itemGap: 16,
      data: ['Synthetic', 'Original'],
      textStyle: { fontSize: 11, color: '#000' }
    },

    /* subplot titles, positioned above each grid */
    graphic: datasets.map((dataset, index) => {
      const row = Math.floor(index / 2)
      const col = index % 2
      return {
        type: 'text',
        left: col === 0 ? '18%' : '64%',
        top: row === 0 ? '9%' : '55%',
        style: {
          text: `${dataset.type} (${dataset.network})`,
          fontSize: 11,
          fontWeight: 600,
          fill: '#24313A'
        }
      }
    }),

    grid: grids,
    xAxis: xAxes,
    yAxis: yAxes,

    tooltip: {
      trigger: 'axis',
      valueFormatter: value => Number(value).toFixed(4)
    },

    series
  }
}

/* =========================================================
   LIFECYCLE
   ========================================================= */

function renderChart() {
  if (!chartRef.value) return
  if (chart) chart.dispose()

  chart = echarts.init(chartRef.value, null, { renderer: 'svg' })
  chart.setOption(buildOption())
}

function resizeChart() {
  requestAnimationFrame(() => chart?.resize())
}

onMounted(async () => {
  await nextTick()
  renderChart()

  resizeObserver = new ResizeObserver(() => resizeChart())
  if (chartRef.value) resizeObserver.observe(chartRef.value)

  window.addEventListener('resize', resizeChart)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeChart)

  if (resizeObserver) {
    resizeObserver.disconnect()
    resizeObserver = null
  }

  if (chart) {
    chart.dispose()
    chart = null
  }
})
</script>

<template>
  <div class="dynamics-slide">
    <div ref="chartRef" class="dynamics-chart"></div>

    <div class="findings">
      <div
        v-for="item in findings"
        :key="item.number"
        class="finding"
      >
        <div class="finding-header">
          <span class="finding-number">{{ item.number }}</span>
          <h3>{{ item.title }}</h3>
        </div>

        <p>{{ item.text }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.dynamics-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.dynamics-chart {
  width: 100%;
  height: 78%;
  min-height: 0;
}

.findings {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 12px;
  margin-top: 10px;
}

.finding { min-width: 0; box-sizing: border-box; padding: 7px 9px; border-top: 2px solid #b3cedf; background: #fff; position: relative; z-index: 1; transition: transform 0.22s ease, box-shadow 0.22s ease, border-top-color 0.22s ease; }

.finding-header {
  display: flex;
  align-items: baseline;
  gap: 6px;
  margin-bottom: 4px;
}

.finding-number {
  flex: 0 0 auto;
  color: #2A9D8F;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: .08em;
}

.finding h3 {
  margin: 0;
  color: #173F5F;
  font-size: 11px;
  line-height: 1.2;
  font-weight: 700;
}

.finding p {
  margin: 0;
  color: #64748B;
  font-size: 9.5px;
  line-height: 1.3;
}
.finding:hover { transform: translateY(-4px); border-top-color: #2A9D8F; box-shadow: 0 7px 16px rgba(23, 63, 95, 0.12), 0 2px 5px rgba(23, 63, 95, 0.06); z-index: 5; }
.finding:hover .finding-number { transform: scale(1.08); color: #20639B; }
.finding:hover h3 { color: #20639B; }

@media (max-width: 1000px) {
  .findings {
    grid-template-columns: repeat(2, 1fr);
  }

  .dynamics-chart {
    height: 62%;
  }
}
</style>