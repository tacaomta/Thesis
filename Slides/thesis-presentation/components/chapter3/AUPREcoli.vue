<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chart10Ref = ref(null)
const chart50Ref = ref(null)
const chart100Ref = ref(null)

let charts = []
let resizeObserver = null

const toy10 = [
  { name: 'Baseline', mean: 0.175, std: 0.053 },
  { name: 'AVG', mean: 0.518, std: 0.251 },
  { name: 'GNB', mean: 0.566, std: 0.171 },
  { name: 'Jump3', mean: 0.174, std: 0.076 },
  { name: 'Inferelator', mean: 0.169, std: 0.079 },
  { name: 'CLR-lag', mean: 0.195, std: 0.071 },
  { name: 'TSNI', mean: 0.214, std: 0.071 },
  { name: 'G1DBN', mean: 0.185, std: 0.071 }
]
const toy50 = [
  { name: 'Baseline', mean: 0.043, std: 0.005 },
  { name: 'AVG', mean: 0.164, std: 0.074 },
  { name: 'GNB', mean: 0.355, std: 0.083 },
  { name: 'Jump3', mean: 0.05, std: 0.006 },
  { name: 'Inferelator', mean: 0.04, std: 0.007 },
  { name: 'CLR-lag', mean: 0.045, std: 0.008 },
  { name: 'TSNI', mean: 0.047, std: 0.007 },
  { name: 'G1DBN', mean: 0.043, std: 0.004 }
]

const toy100 = [
  { name: 'Baseline', mean: 0.025, std: 0.000 },
  { name: 'AVG', mean: 0.111, std: 0.03 },
  { name: 'GNB', mean: 0.324, std: 0.055 },
  { name: 'Jump3', mean: 0.031, std: 0.005 },
  { name: 'Inferelator', mean: 0.027, std: 0.005 },
  { name: 'CLR-lag', mean: 0.025, std: 0.001 },
  { name: 'TSNI', mean: 0.028, std: 0.003 },
  { name: 'G1DBN', mean: 0.027, std: 0.003 }
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
        rotate: 45
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

          label: {
            show: true,
            rotate:90,

            position: 'top',

            formatter: params => {
              const item = data[params.dataIndex]

              return (
                `${item.mean.toFixed(3)}`
              )
            },

            color: '#24313A',
            fontSize: 8,
            lineHeight: 11
          }
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
      title: '(a) Ecoli 10'
    },

    {
      ref: chart50Ref,
      data: toy50,
      title: '(b) Ecoli 50'
    },

    {
      ref: chart100Ref,
      data: toy100,
      title: '(c) Ecoli 100'
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
})


onBeforeUnmount(() => {
  window.removeEventListener(
    'resize',
    resizeCharts
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

    <div class="charts-row">

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

    <div class="result-note">
  <div class="result-item">
    <span class="note-icon">▸</span>
    <div>
      <strong>Substantial performance gain: </strong>
      Supervised classifiers significantly outperform traditional paradigms (Jump3, Inferelator, CLR-lag, TSNI, G1DBN).
    </div>
  </div>

  <div class="result-item">
    <span class="note-icon">▸</span>
    <div>
      <strong>Quantitative edge (|V|=10): </strong>
     Average ML AUPR reaches 0.518, compared to Jump3 (0.174) and Inferelator (0.169).
    </div>
  </div>

  <div class="result-item">
    <span class="note-icon">▸</span>
    <div>
      <strong>Consistent top performer: </strong>
      GNB maintains the highest, most stable AUPR across all network scales (0.566 at size 10; 0.324 at size 100).
    </div>
  </div>
</div>

  </div>
</template>


<style scoped>
.aupr-results {
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
   ========================================================= */

.charts-row {
  flex: 1;
  min-height: 0;

  display: grid;

  grid-template-columns:
    repeat(3, minmax(0, 1fr));

  /* reduced from 18px */
  gap: 8px;

  width: 100%;
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
  background: #F8FAFB;
  border: 1px solid #DCE4E9;
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
  color: #24313A;
  font-weight: 600;
}

.note-icon {
  flex-shrink: 0;
  color: #20639B;
  font-size: 14px;
  font-weight: 700;
  line-height: 1.4;
  margin-top: 1px;
}


/* =========================================================
   RESPONSIVE
   ========================================================= */

@media (max-width: 900px) {

  .charts-row {
    gap: 4px;
  }

  .aupr-results {
    padding-left: 2px;
    padding-right: 2px;
  }
}
</style>