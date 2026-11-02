<script setup>
import { ref, computed, onMounted, onBeforeUnmount, nextTick, watch } from 'vue'
import * as echarts from 'echarts'
import { useNav } from '@slidev/client'

const chart10Ref = ref(null)
const chart50Ref = ref(null)
const chart100Ref = ref(null)

let charts = []
let resizeObserver = null

/* ============================================================
 * REVEAL STATE — SPACE reveals one finding card at a time.
 * The chart area shrinks as soon as the first card appears,
 * and stays shrunk as long as any card is visible.
 * ============================================================ */

const { currentPage } = useNav()

const visibleCount = ref(0)
const totalFindings = 3

const notesVisible = computed(() => visibleCount.value > 0)

watch(currentPage, () => {
  visibleCount.value = 0
})

function revealNext() {
  visibleCount.value =
    visibleCount.value < totalFindings
      ? visibleCount.value + 1
      : 0

  /*
   * The charts-row container changes height when the note
   * area is shown/hidden, so the charts must be explicitly
   * resized after the DOM has updated — ResizeObserver alone
   * may not fire reliably on a flex-basis change in some
   * browsers.
   */
  nextTick(() => {
    resizeCharts()
  })
}

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  revealNext()
}


/* ============================================================
 * DATA
 * ============================================================ */

const toy10 = [
  { name: 'Baseline', mean: 0.268, std: 0.034 },
  { name: 'LR', mean: 0.283, std: 0.057 },
  { name: 'DT', mean: 0.446, std: 0.076 },
  { name: 'RF', mean: 0.602, std: 0.093 },
  { name: 'XGB', mean: 0.323, std: 0.061 },
  { name: 'LGB', mean: 0.413, std: 0.079 },
  { name: 'GNB', mean: 0.398, std: 0.141 },
  { name: 'KNN', mean: 0.411, std: 0.171 },
  { name: 'MLP', mean: 0.566, std: 0.097 },
]

const toy50 = [
  { name: 'Baseline', mean: 0.048, std: 0.003 },
  { name: 'LR', mean: 0.05, std: 0.005 },
  { name: 'DT', mean: 0.132, std: 0.024 },
  { name: 'RF', mean: 0.515, std: 0.053 },
  { name: 'XGB', mean: 0.061, std: 0.007 },
  { name: 'LGB', mean: 0.127, std: 0.024 },
  { name: 'GNB', mean: 0.48, std: 0.138 },
  { name: 'KNN', mean: 0.273, std: 0.224 },
  { name: 'MLP', mean: 0.329, std: 0.045 },
]

const toy100 = [
  { name: 'Baseline', mean: 0.023, std: 0.001 },
  { name: 'LR', mean: 0.025, std: 0.002 },
  { name: 'DT', mean: 0.096, std: 0.015 },
  { name: 'RF', mean: 0.503, std: 0.058 },
  { name: 'XGB', mean: 0.03, std: 0.003 },
  { name: 'LGB', mean: 0.072, std: 0.012 },
  { name: 'GNB', mean: 0.511, std: 0.001 },
  { name: 'KNN', mean: 0.1, std: 0.112 },
  { name: 'MLP', mean: 0.288, std: 0.034 },
]


function createOption(data, title) {
  const names = data.map(item => item.name)
  const means = data.map(item => item.mean)

  const maxValue = Math.max(
    ...data.map(item => item.mean + item.std),
    0.1
  )

  return {
    animation: false,

    grid: {
      left: 42,
      right: 12,
      top: 48,
      bottom: 55,
      containLabel: true
    },

    title: {
      text: title,
      left: 'center',
      top: 4,

      textStyle: {
        fontSize: 15,
        fontWeight: 600,
        color: '#24313A'
      }
    },

    xAxis: {
      type: 'category',
      data: names,

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
        fontSize: 9,
        interval: 0,
        rotate: 0
      }
    },

    yAxis: {
      type: 'value',

      min: 0,

      max: Math.min(
        1,
        Math.ceil(maxValue * 10) / 10
      ),

      interval: 0.2,

      name: 'Performance',
      nameLocation: 'middle',
      nameGap: 34,

      nameTextStyle: {
        color: '#475569',
        fontSize: 9
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
        fontSize: 9,

        formatter: value =>
          value.toFixed(1)
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
        const item = data[index]

        return `
          <div style="font-size:12px; line-height:1.6">
            <strong>${item.name}</strong><br/>
            Mean: ${item.mean.toFixed(3)}<br/>
            Std: ±${item.std.toFixed(3)}
          </div>
        `
      }
    },

    series: [

      /* ================================
         BAR
         ================================ */

      {
        type: 'bar',

        data: means.map(value => ({
          value,

          itemStyle: {
            color: '#08B6F3'
          },
        })),

        barMaxWidth: 38,

        /*
         * No border around bars.
         */
        itemStyle: {
          borderWidth: 0
        },

        z: 2
      },


      /* ================================
         ERROR BAR — STANDARD DEVIATION
         ================================ */

      {
        type: 'custom',

        data: data.map((item, index) => [
          index,
          item.mean,
          item.std
        ]),

        renderItem(params, api) {
          const index = api.value(0)
          const mean = api.value(1)
          const std = api.value(2)

          const x = api.coord([
            index,
            mean
          ])[0]

          const yTop = api.coord([
            index,
            mean + std
          ])[1]

          const yBottom = api.coord([
            index,
            Math.max(0, mean - std)
          ])[1]

          const capWidth = 6

          return {
            type: 'group',

            children: [

              /* vertical STD line */

              {
                type: 'line',

                shape: {
                  x1: x,
                  y1: yTop,
                  x2: x,
                  y2: yBottom
                },

                style: {
                  stroke: '#EB5F34',
                  lineWidth: 1
                }
              },

              /* upper cap */

              {
                type: 'line',

                shape: {
                  x1: x - capWidth,
                  y1: yTop,
                  x2: x + capWidth,
                  y2: yTop
                },

                style: {
                  stroke: '#EB5F34',
                  lineWidth: 1
                }
              },

              /* lower cap */

              {
                type: 'line',

                shape: {
                  x1: x - capWidth,
                  y1: yBottom,
                  x2: x + capWidth,
                  y2: yBottom
                },

                style: {
                  stroke: '#EB5F34',
                  lineWidth: 1
                }
              }
            ]
          }
        },

        z: 5,

        tooltip: {
          show: false
        }
      }
    ]
  }
}


async function initCharts() {
  await nextTick()

  charts.forEach(chart => {
    chart.dispose()
  })

  charts = []

  const configs = [
    {
      ref: chart10Ref,
      data: toy10,
      title: '(a) Size 10'
    },

    {
      ref: chart50Ref,
      data: toy50,
      title: '(b) Size 50'
    },

    {
      ref: chart100Ref,
      data: toy100,
      title: '(c) Size 100'
    }
  ]

  configs.forEach(({ ref, data, title }) => {
    if (!ref.value || !data.length) return

    const chart = echarts.init(
      ref.value,
      null,
      {
        renderer: 'svg'
      }
    )

    chart.setOption(
      createOption(data, title)
    )

    chart.resize()

    charts.push(chart)
  })
}


function resizeCharts() {
  requestAnimationFrame(() => {
    charts.forEach(chart => {
      chart.resize()
    })
  })
}


onMounted(async () => {
  await initCharts()

  resizeObserver = new ResizeObserver(() => {
    resizeCharts()
  })

  ;[
    chart10Ref,
    chart50Ref,
    chart100Ref
  ].forEach(ref => {
    if (ref.value) {
      resizeObserver.observe(ref.value)
    }
  })

  window.addEventListener(
    'resize',
    resizeCharts
  )

  window.addEventListener(
    'keydown',
    handleKeydown,
    true
  )
})


onBeforeUnmount(() => {
  window.removeEventListener(
    'resize',
    resizeCharts
  )

  window.removeEventListener(
    'keydown',
    handleKeydown,
    true
  )

  if (resizeObserver) {
    resizeObserver.disconnect()
  }

  charts.forEach(chart => {
    chart.dispose()
  })

  charts = []
})
</script>


<template>
  <div class="aupr-results">

    <div class="charts-row" :class="{ 'note-open': notesVisible }">

      <div class="chart-card">
        <div
          ref="chart10Ref"
          class="chart"
        ></div>
      </div>

      <div class="chart-card">
        <div
          ref="chart50Ref"
          class="chart"
        ></div>
      </div>

      <div class="chart-card">
        <div
          ref="chart100Ref"
          class="chart"
        ></div>
      </div>

    </div>

    <div v-if="notesVisible" class="findings">

      <Transition name="card-pop">
        <div v-if="visibleCount >= 1" class="finding">
          <div class="finding-header">
            <span class="finding-number">01</span>
            <h3>Universal baseline superiority</h3>
          </div>
          <p>
            All evaluated machine learning models outperform the random baseline across all network scales.
          </p>
        </div>
      </Transition>

      <Transition name="card-pop">
        <div v-if="visibleCount >= 2" class="finding">
          <div class="finding-header">
            <span class="finding-number">02</span>
            <h3>Ensemble model dominance</h3>
          </div>
          <p>
            Random Forest achieves top average AUPR across all network sizes (0.602 at size 10; 0.503 at size 100).
          </p>
        </div>
      </Transition>

      <Transition name="card-pop">
        <div v-if="visibleCount >= 3" class="finding">
          <div class="finding-header">
            <span class="finding-number">03</span>
            <h3>Probabilistic resilience</h3>
          </div>
          <p>
            GNB exhibits scale-resilient performance improvements as network size increases.
          </p>
        </div>
      </Transition>

    </div>

  </div>
</template>


<style scoped>
.aupr-results {
  position: relative;

  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 8px 6px 0;
}


/* =========================================================
   THREE CHARTS — CLOSER TOGETHER
   Takes the FULL height by default (notes hidden); shrinks
   only once the first finding card is revealed.
   ========================================================= */

.charts-row {
  flex: 1;
  min-height: 0;

  display: grid;

  grid-template-columns:
    repeat(3, minmax(0, 1fr));

  gap: 8px;

  width: 100%;

  transition: flex-basis 0.25s ease;
}


.chart-card {
  min-width: 0;
  min-height: 0;

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
   FINDINGS — horizontal row of cards, revealed one at a time
   via SPACE
   ========================================================= */

.findings {
  flex-shrink: 0;

  width: 100%;

  display: grid;
  grid-template-columns: repeat(3, 1fr);

  gap: 10px;

  margin: 8px auto 4px;
}

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

.finding:hover {
  transform: translateY(-4px);

  border-top-color: #2a9d8f;

  box-shadow:
    0 7px 16px rgba(23, 63, 95, 0.12),
    0 2px 5px rgba(23, 63, 95, 0.06);

  z-index: 5;
}

.finding:hover .finding-number {
  transform: scale(1.08);
  color: #20639b;
}

.finding:hover h3 {
  color: #20639b;
}

.finding-header {
  display: flex;
  align-items: baseline;
  gap: 6px;

  margin-bottom: 4px;
}

.finding-number {
  flex: 0 0 auto;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.08em;

  transition: transform 0.22s ease, color 0.22s ease;
}

.finding h3 {
  margin: 0;

  color: #173f5f;

  font-size: 11.5px;
  line-height: 1.2;
  font-weight: 700;

  transition: color 0.22s ease;
}

.finding p {
  margin: 0;

  color: #64748b;

  font-size: 10px;
  line-height: 1.35;
}

/*
 * Each card pops in individually as visibleCount increases.
 */

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

  .charts-row {
    gap: 4px;
  }

  .findings {
    grid-template-columns: 1fr;
  }

  .aupr-results {
    padding-left: 2px;
    padding-right: 2px;
  }
}
</style>