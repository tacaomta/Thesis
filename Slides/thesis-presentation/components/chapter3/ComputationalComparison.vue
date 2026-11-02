<script setup>
import {
  ref,
  computed,
  onMounted,
  onBeforeUnmount,
  nextTick,
  watch
} from 'vue'

import * as echarts from 'echarts'
import { useNav } from '@slidev/client'

const chartRef = ref(null)

let chart = null
let resizeObserver = null

// ============================================================
// REVEAL STATE — SPACE reveals one finding card at a time.
// ============================================================

const { currentPage } = useNav()

const visibleCount = ref(0)
const totalNotes = 2

const notesVisible = computed(() => visibleCount.value > 0)

watch(currentPage, () => {
  visibleCount.value = 0

  nextTick(() => {
    resizeChart()
  })
})

function revealNext() {
  visibleCount.value =
    visibleCount.value < totalNotes
      ? visibleCount.value + 1
      : 0

  nextTick(() => {
    resizeChart()
  })
}

function handleKeydown(event) {
  if (event.code !== 'Space') return

  const target = event.target

  // Do not intercept Space when interacting with controls.
  if (
    target instanceof HTMLElement &&
    (
      target.isContentEditable ||
      ['INPUT', 'TEXTAREA', 'SELECT', 'BUTTON'].includes(target.tagName)
    )
  ) {
    return
  }

  event.preventDefault()
  event.stopPropagation()

  revealNext()
}


// ============================================================
// DATA — Training / Testing time (log10 ms) per algorithm
// ============================================================

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


// ============================================================
// OPTION BUILDER
// ============================================================

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
        lineStyle: {
          color: '#64748B',
          width: 1
        }
      },

      axisTick: {
        show: true,
        alignWithLabel: true,
        lineStyle: {
          color: '#64748B',
          width: 1
        }
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
        lineStyle: {
          color: '#64748B',
          width: 1
        }
      },

      axisTick: {
        show: true,
        lineStyle: {
          color: '#64748B',
          width: 1
        }
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


// ============================================================
// LIFECYCLE
// ============================================================

async function initChart() {
  await nextTick()

  if (chart) {
    chart.dispose()
    chart = null
  }

  if (!chartRef.value) return

  chart = echarts.init(
    chartRef.value,
    null,
    { renderer: 'svg' }
  )

  chart.setOption(createOption())
  chart.resize()
}

function resizeChart() {
  requestAnimationFrame(() => {
    if (chart) {
      chart.resize()
    }
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
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeChart)
  window.removeEventListener('keydown', handleKeydown, true)

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

    <!-- HEADER + LEGEND -->
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


    <!-- CHART -->
    <div class="chart-card">
      <div ref="chartRef" class="chart"></div>
    </div>


    <!-- FINDINGS — HORIZONTAL CARDS -->
    <div v-if="notesVisible" class="findings">

      <!-- Finding 01 -->
      <Transition name="card-pop">
        <div v-if="visibleCount >= 1" class="finding">

          <div class="finding-header">
            <span class="finding-number">01</span>
            <h3>Ultra-fast online inference</h3>
          </div>

          <p>
            Once trained, supervised classifiers execute inference
            orders of magnitude faster than non-learning end-to-end methods.
          </p>

        </div>
      </Transition>


      <!-- Finding 02 -->
      <Transition name="card-pop">
        <div v-if="visibleCount >= 2" class="finding">

          <div class="finding-header">
            <span class="finding-number">02</span>
            <h3>Favorable scalability</h3>
          </div>

          <p>
            Offloads heavy computation to offline training,
            enabling rapid online network reconstruction.
          </p>

        </div>
      </Transition>

    </div>

  </div>
</template>


<style scoped>

/* =========================================================
   MAIN CONTAINER
   ========================================================= */

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
   Takes the available height when notes are hidden.
   Shrinks automatically when finding cards are revealed.
   ========================================================= */

.chart-card {
  flex: 1 1 0;

  min-height: 0;
  min-width: 0;

  display: flex;
  align-items: stretch;
  justify-content: center;

  transition: flex 0.25s ease;
}

.chart {
  width: 100%;
  height: 100%;
  min-height: 0;
}


/* =========================================================
   FINDINGS — HORIZONTAL ROW OF CARDS
   Adapted from reference file 1
   ========================================================= */

.findings {
  flex-shrink: 0;

  width: 100%;

  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));

  gap: 10px;

  margin: 8px auto 4px;
}


/* Individual finding card */

.finding {
  min-width: 0;

  box-sizing: border-box;

  padding: 9px 11px;

  border-top: 2px solid #b3cedf;

  background: #ffffff;

  position: relative;
  z-index: 1;

  transition:
    transform 0.22s ease,
    box-shadow 0.22s ease,
    border-top-color 0.22s ease;
}


/* Hover effect */

.finding:hover {
  transform: translateY(-4px);

  border-top-color: #2a9d8f;

  box-shadow:
    0 7px 16px rgba(23, 63, 95, 0.12),
    0 2px 5px rgba(23, 63, 95, 0.06);

  z-index: 5;
}


/* Card header */

.finding-header {
  display: flex;
  align-items: baseline;

  gap: 6px;

  margin-bottom: 4px;
}


/* Number */

.finding-number {
  flex: 0 0 auto;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.08em;

  transition:
    transform 0.22s ease,
    color 0.22s ease;
}


/* Title */

.finding h3 {
  margin: 0;

  color: #173f5f;

  font-size: 11.5px;
  line-height: 1.2;
  font-weight: 700;

  transition: color 0.22s ease;
}


/* Description */

.finding p {
  margin: 0;

  color: #64748b;

  font-size: 10px;
  line-height: 1.35;
}


/* Hover details */

.finding:hover .finding-number {
  transform: scale(1.08);
  color: #20639b;
}

.finding:hover h3 {
  color: #20639b;
}


/* =========================================================
   CARD REVEAL ANIMATION
   ========================================================= */

.card-pop-enter-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.card-pop-enter-from {
  opacity: 0;
  transform: translateY(10px);
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

  .findings {
    grid-template-columns: 1fr;
  }

}

</style> 