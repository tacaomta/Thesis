<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)

let chart = null
let resizeObserver = null

/* =========================================================
   DATA — Training / Testing time (log10 ms) per algorithm
   ========================================================= */

const algorithms = [
  'LR', 'DT', 'RF', 'KNN',
  'XGB', 'LGB', 'MLP', 'GNB',
  'Jump3', 'Inferelator', 'CLR-lag', 'TSNI', 'G1DBN'
]

const training = [
  4.420907685, 7.208711517, 7.866217595, 4.02432008,
  5.151441361, 5.002477144, 8.100016463, 4.27000026,
  7.248061554, 4.551464789, 4.803339645, 1.991258868, 4.307885359
]

const testing = [
  1.093845327, 1.72182865, 3.612969958, 6.331371373,
  1.161079355, 1.593983591, 4.046033227, 2.037724549,
  null, null, null, null, null
]

const COLOR_TRAIN = '#08B6F3'
const COLOR_TEST = '#FFA500'
const COLOR_E2E = '#ECB60D'

/* =========================================================
   OPTION BUILDER
   ========================================================= */

function createOption() {
  const trainingSeriesData = training.map((value, i) => ({
    value,
    itemStyle: {
      color: testing[i] === null ? COLOR_E2E : COLOR_TRAIN,
      borderWidth: 0
    },
    label: {
      show: true,
      position: 'inside',
      formatter: () => value.toFixed(2),
      color: '#ffffff',
      fontSize: 9,
      fontWeight: 600
    }
  }))

  const testingSeriesData = testing.map((value) => {
    if (value === null) {
      return {
        value: 0,
        itemStyle: { color: 'transparent' },
        label: { show: false },
        tooltip: { show: false }
      }
    }

    return {
      value,
      itemStyle: {
        color: COLOR_TEST,
        borderWidth: 0
      },
      label: {
        show: true,
        position: 'inside',
        formatter: () => value.toFixed(2),
        color: '#ffffff',
        fontSize: 9,
        fontWeight: 600
      }
    }
  })

  return {
    animation: false,

    grid: {
      left: 48,
      right: 16,
      top: 20,
      bottom: 70,
      containLabel: true
    },

    xAxis: {
      type: 'category',
      data: algorithms,

      axisLine: {
        show: true,
        lineStyle: { color: '#64748B', width: 1 }
      },

      axisTick: {
        show: true,
        alignWithLabel: true,
        lineStyle: { color: '#64748B', width: 1 }
      },

      axisLabel: {
        color: '#475569',
        fontSize: 10,
        interval: 0,
        rotate: 45
      }
    },

    yAxis: {
      type: 'value',

      name: 'log10(time in ms)',
      nameLocation: 'middle',
      nameGap: 36,

      nameTextStyle: {
        color: '#475569',
        fontSize: 11,
        fontWeight: 600
      },

      axisLine: {
        show: true,
        lineStyle: { color: '#64748B', width: 1 }
      },

      axisTick: {
        show: true,
        lineStyle: { color: '#64748B', width: 1 }
      },

      axisLabel: {
        color: '#475569',
        fontSize: 10
      },

      splitLine: {
        show: true,
        lineStyle: {
          color: '#E2E8F0',
          type: 'dashed',
          width: 1
        }
      }
    },

    tooltip: {
      trigger: 'axis',

      axisPointer: {
        type: 'shadow'
      },

      formatter: params => {
        const index = params[0].dataIndex
        const name = algorithms[index]
        const train = training[index]
        const test = testing[index]

        if (test === null) {
          return `
            <div style="font-size:12px; line-height:1.6">
              <strong>${name}</strong><br/>
              End-to-end inference: ${train.toFixed(3)}
            </div>
          `
        }

        return `
          <div style="font-size:12px; line-height:1.6">
            <strong>${name}</strong><br/>
            Training: ${train.toFixed(3)}<br/>
            Testing: ${test.toFixed(3)}
          </div>
        `
      }
    },

    series: [
      {
        name: 'Training',
        type: 'bar',
        stack: 'total',
        barMaxWidth: 30,
        data: trainingSeriesData,
        z: 2
      },
      {
        name: 'Testing',
        type: 'bar',
        stack: 'total',
        barMaxWidth: 30,
        data: testingSeriesData,
        z: 2
      }
    ]
  }
}

/* =========================================================
   LIFECYCLE
   ========================================================= */

async function initChart() {
  await nextTick()

  if (chart) {
    chart.dispose()
    chart = null
  }

  if (!chartRef.value) return

  chart = echarts.init(chartRef.value, null, { renderer: 'svg' })
  chart.setOption(createOption())
  chart.resize()
}

function resizeChart() {
  requestAnimationFrame(() => {
    if (chart) chart.resize()
  })
}

onMounted(async () => {
  await initChart()

  resizeObserver = new ResizeObserver(() => {
    resizeChart()
  })

  if (chartRef.value) {
    resizeObserver.observe(chartRef.value)
  }

  window.addEventListener('resize', resizeChart)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeChart)

  if (resizeObserver) {
    resizeObserver.disconnect()
  }

  if (chart) {
    chart.dispose()
    chart = null
  }
})
</script>

<template>
  <div class="runtime-results">

    <div class="chart-header">
      <h2></h2>

      <div class="legend-row">
        <div class="legend-item">
          <span class="legend-dot train-dot"></span>
          Training
        </div>

        <div class="legend-item">
          <span class="legend-dot test-dot"></span>
          Testing
        </div>

        <div class="legend-item">
          <span class="legend-dot e2e-dot"></span>
          End-to-end inference time
        </div>
      </div>
    </div>

    <div class="chart-card">
      <div ref="chartRef" class="chart"></div>
    </div>

    <div class="result-note">
      <div class="result-item">
        <span class="note-icon">▸</span>
        <div>
          <strong>Reduced training time: </strong>
          Training on 20,000 small |V|=10 networks reduces training duration by 15%–25% compared to training on large networks.
        </div>
      </div>

      <div class="result-item">
        <span class="note-icon">▸</span>
        <div>
          <strong>Ultra-fast online inference: </strong>
          Once trained, supervised classifiers execute inference orders of magnitude faster than non-learning end-to-end methods.
        </div>
      </div>

      <div class="result-item">
        <span class="note-icon">▸</span>
        <div>
          <strong>Favorable scalability: </strong>
          Offloads heavy computation to offline training, enabling rapid online network reconstruction.
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped>
.runtime-results {
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 8px 6px 0;
  margin-top: 10px;
}

/* =========================================================
   HEADER + LEGEND
   ========================================================= */

.chart-header {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  justify-content: space-between;

  gap: 12px;

  margin-bottom: 6px;
}

.chart-header h2 {
  margin: 0;

  color: #24313a;

  font-size: 16px;
  font-weight: 650;

  white-space: nowrap;
}

.legend-row {
  display: flex;
  align-items: center;

  gap: 14px;
}

.legend-item {
  display: flex;
  align-items: center;

  gap: 6px;

  color: #64748b;

  font-size: 10.5px;

  white-space: nowrap;
}

.legend-dot {
  width: 8px;
  height: 8px;

  flex-shrink: 0;

  border-radius: 2px;
}

.train-dot {
  background: #08b6f3;
}

.test-dot {
  background: #ffa500;
}

.e2e-dot {
  background: #ecb60d;
}

/* =========================================================
   CHART
   ========================================================= */

.chart-card {
  flex: 1;
  min-height: 0;
  min-width: 0;

  display: flex;
  align-items: stretch;
  justify-content: center;
}

.chart {
  width: 100%;
  height: 100%;
  min-height: 0;
}

/* =========================================================
   CONCLUSION
   ========================================================= */

.result-note {
  flex-shrink: 0;

  display: flex;
  flex-direction: column;

  gap: 6px;

  margin: 5px auto 2px;

  width: min(100%, 1000px);

  padding: 5px 10px;

  box-sizing: border-box;

  background: #f8fafb;

  border: 1px solid #dce4e9;
  border-radius: 6px;

  color: #475569;

  font-size: 12px;
  line-height: 1.4;

  border-left: 5px #259b37 solid;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.result-item {
  display: flex;
  align-items: flex-start;

  gap: 5px;
}

.result-item strong {
  color: #24313a;
  font-weight: 600;
}

.note-icon {
  flex-shrink: 0;

  color: #20639b;

  font-size: 14px;
  font-weight: 700;
  line-height: 1.4;

  margin-top: 1px;
}

/* =========================================================
   RESPONSIVE
   ========================================================= */

@media (max-width: 900px) {

  .chart-header {
    flex-direction: column;
    align-items: flex-start;

    gap: 6px;
  }

  .runtime-results {
    padding-left: 2px;
    padding-right: 2px;
  }
}
</style>