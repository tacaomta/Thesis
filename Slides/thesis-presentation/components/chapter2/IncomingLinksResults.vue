<template>
  <div class="results-slide">
    <div class="chart-header">
      <div>
        <div class="chart-description">
          Performance as the number of incoming regulatory links to a target gene increases.
        </div>
      </div>

      <div class="dataset-badge">
        <span>Target gene difficulty</span>
        <span class="dot">·</span>
        <span>D = 1–8</span>
      </div>
    </div>

    <div ref="chartRef" class="chart"></div>

    <div class="bottom-message">
      <span class="message-mark"></span>

      <span>
        Increasing incoming links makes GRN inference substantially more difficult,
        while dynamic and structural accuracy remain comparatively robust.
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)

let chart = null
let resizeObserver = null

/* =========================================================
   DATA
   ========================================================= */

const xAxisData = [1, 2, 3, 4, 5, 6, 7, 8]

const dynamic    = [100, 100, 100, 100, 100, 100, 100, 99.6]
const precision  = [100, 96.5, 26.25, 13.4, 12.8, 13.85, 15.2, 13.85]
const recall     = [100, 97.8, 32.4, 13.15, 10, 9.05, 8.55, 2.85]
const structural = [100, 99.85, 90.25, 86.05, 83.9, 81.85, 80.1, 78]

const toNormalized = values => values.map(value => value / 100)

/* =========================================================
   SERIES HELPER
   ========================================================= */

function lineSeries(name, data, color, symbol, symbolSize) {
  return {
    name,
    type: 'line',
    data: toNormalized(data),
    smooth: false,
    symbol,
    symbolSize,
    showSymbol: true,
    lineStyle: { width: 2.5, color },
    itemStyle: { color },
    emphasis: {
      focus: 'series',
      lineStyle: { width: 4 },
      symbolSize: symbolSize + 3
    }
  }
}

/* shared axis line / tick style */
const axisLineStyle = { color: '#94A3B8', width: 1 }

/* =========================================================
   OPTION
   ========================================================= */

function buildOption() {
  return {
    animation: true,
    animationDuration: 900,
    animationEasing: 'cubicOut',

    grid: {
      left: 75,
      right: 30,
      top: 58,
      bottom: 62,
      containLabel: true
    },

    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'line',
        lineStyle: { color: '#94A3B8', width: 1, type: 'dashed' }
      },
      backgroundColor: 'rgba(255, 255, 255, 0.97)',
      borderColor: '#DCE4E9',
      borderWidth: 1,
      textStyle: { color: '#24313A', fontSize: 12 },
      padding: [10, 14],

      formatter(params) {
        if (!params || !params.length) return ''

        let html = `
          <div style="font-weight:600; margin-bottom:7px;">
            Incoming links: ${params[0].axisValue}
          </div>
        `

        params.forEach(item => {
          html += `
            <div style="display:flex; align-items:center; gap:7px; margin:4px 0;">
              <span style="display:inline-block; width:8px; height:8px; border-radius:2px; background:${item.color};"></span>
              <span style="flex:1;">${item.seriesName}</span>
              <strong style="margin-left:14px;">${Number(item.value).toFixed(2)}</strong>
            </div>
          `
        })

        return html
      }
    },

    legend: {
      top: 8,
      left: 'center',
      itemWidth: 20,
      itemHeight: 3,
      itemGap: 24,
      selectedMode: true,
      textStyle: { color: '#475569', fontSize: 12, fontWeight: 500 }
    },

    xAxis: {
      type: 'category',
      boundaryGap: false,
      data: xAxisData,

      name: 'Number of incoming links (D)',
      nameLocation: 'middle',
      nameGap: 38,
      nameTextStyle: { color: '#64748B', fontSize: 11 },

      axisLine: { show: true, lineStyle: axisLineStyle },
      axisTick: {
        show: true,
        alignWithLabel: true,
        length: 6,
        lineStyle: axisLineStyle
      },
      axisLabel: {
        show: true,
        color: '#64748B',
        fontSize: 11,
        interval: 0,
        margin: 10
      },
      splitLine: { show: false }
    },

    yAxis: {
      type: 'value',
      min: 0,
      max: 1,
      interval: 0.1,

      name: 'Performance metrics',
      nameLocation: 'middle',
      nameGap: 48,
      nameTextStyle: { color: '#64748B', fontSize: 11, fontWeight: 500 },

      axisLine: { show: true, lineStyle: axisLineStyle },
      axisTick: { show: true, length: 6, lineStyle: axisLineStyle },
      axisLabel: {
        show: true,
        color: '#64748B',
        fontSize: 10,
        formatter: value => value.toFixed(1)
      },
      splitLine: {
        show: true,
        lineStyle: { color: '#E8EDF1', width: 1, type: 'solid' }
      }
    },

    series: [
      lineSeries('Precision',           precision,  '#E76F51', 'circle',   8),
      lineSeries('Recall',              recall,     '#2A9D8F', 'diamond',  9),
      lineSeries('Dynamic Accuracy',    dynamic,    '#20639B', 'triangle', 10),
      lineSeries('Structural Accuracy', structural, '#7A5AF8', 'rect',     8)
    ]
  }
}

/* =========================================================
   LIFECYCLE
   ========================================================= */

function hasSize(el) {
  return !!el && el.clientWidth > 0 && el.clientHeight > 0
}

/* Only create the chart once the container has a real size */
function ensureChart() {
  const el = chartRef.value
  if (!hasSize(el)) return

  if (!chart) {
    chart = echarts.init(el, null, { renderer: 'svg' })
    chart.setOption(buildOption())
  } else {
    chart.resize()
  }
}

function handleResize() {
  requestAnimationFrame(ensureChart)
}

onMounted(async () => {
  await nextTick()

  /* try immediately (works if layout is already settled) */
  ensureChart()

  /* fires as soon as the container gets / changes its size,
     which covers the first-load case where size is initially 0 */
  resizeObserver = new ResizeObserver(handleResize)
  if (chartRef.value) resizeObserver.observe(chartRef.value)

  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)

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

<style scoped>
.results-slide {
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 4px 0 0;
}

.chart-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;

  gap: 30px;

  flex-shrink: 0;
}

.chart-description {
  color: #64748B;

  font-size: 13px;
  line-height: 1.4;
}

.dataset-badge {
  display: flex;
  align-items: center;

  gap: 7px;

  padding: 6px 11px;

  border: 1px solid #DCE4E9;
  border-radius: 6px;

  background: #F8FAFB;

  color: #64748B;

  font-size: 10px;

  white-space: nowrap;
}

.dot {
  color: #94A3B8;
}

.chart {
  width: 100%;

  flex: 1;

  /* min-width/min-height keep the flex child measurable */
  min-width: 0;
  min-height: 200px;

  margin-top: 4px;
}

.bottom-message {
  flex-shrink: 0;

  display: flex;
  align-items: center;

  gap: 10px;

  margin-top: 3px;

  padding: 9px 14px;

  border-left: 3px solid #20639B;

  background: #F3F7FA;

  color: #475569;

  font-size: 11px;
  line-height: 1.35;
}

.message-mark {
  width: 6px;
  height: 6px;

  flex-shrink: 0;

  border-radius: 50%;

  background: #20639B;
}
</style>