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
import { ref, onMounted, onBeforeUnmount } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)

let chart = null

const xAxis = [1, 2, 3, 4, 5, 6, 7, 8]

const dynamic = [
  100,
  100,
  100,
  100,
  100,
  100,
  100,
  99.6
]

const precision = [
  100,
  96.5,
  26.25,
  13.4,
  12.8,
  13.85,
  15.2,
  13.85
]

const recall = [
  100,
  97.8,
  32.4,
  13.15,
  10,
  9.05,
  8.55,
  2.85
]

const structural = [
  100,
  99.85,
  90.25,
  86.05,
  83.9,
  81.85,
  80.1,
  78
]

const toNormalized = values =>
  values.map(value => value / 100)

function createChart() {
  if (!chartRef.value) return

  chart = echarts.init(chartRef.value)

  const option = {
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

        lineStyle: {
          color: '#94A3B8',
          width: 1,
          type: 'dashed'
        }
      },

      backgroundColor: 'rgba(255, 255, 255, 0.97)',

      borderColor: '#DCE4E9',

      borderWidth: 1,

      textStyle: {
        color: '#24313A',
        fontSize: 12
      },

      padding: [10, 14],

      formatter(params) {
        if (!params || !params.length) {
          return ''
        }

        const incomingLinks = params[0].axisValue

        let html = `
          <div style="
            font-weight:600;
            margin-bottom:7px;
          ">
            Incoming links: ${incomingLinks}
          </div>
        `

        params.forEach(item => {
          const value = Number(item.value)

          html += `
            <div style="
              display:flex;
              align-items:center;
              gap:7px;
              margin:4px 0;
            ">
              <span style="
                display:inline-block;
                width:8px;
                height:8px;
                border-radius:2px;
                background:${item.color};
              "></span>

              <span style="flex:1;">
                ${item.seriesName}
              </span>

              <strong style="margin-left:14px;">
                ${(value).toFixed(2)}
              </strong>
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

      textStyle: {
        color: '#475569',

        fontSize: 12,

        fontWeight: 500
      },

      selectedMode: true
    },

    xAxis: {
      type: 'category',

      boundaryGap: false,

      data: xAxis,

      name: 'Number of incoming links (D)',

      nameLocation: 'middle',

      nameGap: 38,

      nameTextStyle: {
        color: '#64748B',

        fontSize: 11
      },

      axisLine: {
        show: true,

        lineStyle: {
          color: '#94A3B8',

          width: 1
        }
      },

      axisTick: {
        show: true,

        alignWithLabel: true,

        length: 6,

        lineStyle: {
          color: '#94A3B8',

          width: 1
        }
      },

      axisLabel: {
        show: true,

        color: '#64748B',

        fontSize: 11,

        interval: 0,

        margin: 10,

        formatter(value) {
          return value
        }
      },

      splitLine: {
        show: false
      }
    },

    yAxis: {
      type: 'value',

      min: 0,

      max: 1,

      interval: 0.1,

      name: 'Performance metrics',

      nameLocation: 'middle',

      nameGap: 48,

      nameTextStyle: {
        color: '#64748B',

        fontSize: 11,

        fontWeight: 500
      },

      axisLine: {
        show: true,

        lineStyle: {
          color: '#94A3B8',

          width: 1
        }
      },

      axisTick: {
        show: true,

        length: 6,

        lineStyle: {
          color: '#94A3B8',

          width: 1
        }
      },

      axisLabel: {
        show: true,

        color: '#64748B',

        fontSize: 10,

        formatter(value) {
          return value.toFixed(1)
        }
      },

      splitLine: {
        show: true,

        lineStyle: {
          color: '#E8EDF1',

          width: 1,

          type: 'solid'
        }
      }
    },

    series: [
      {
        name: 'Precision',

        type: 'line',

        data: toNormalized(precision),

        smooth: false,

        symbol: 'circle',

        symbolSize: 8,

        showSymbol: true,

        lineStyle: {
          width: 2.5,

          color: '#E76F51'
        },

        itemStyle: {
          color: '#E76F51'
        },

        emphasis: {
          focus: 'series',

          lineStyle: {
            width: 4
          },

          symbolSize: 11
        }
      },

      {
        name: 'Recall',

        type: 'line',

        data: toNormalized(recall),

        smooth: false,

        symbol: 'diamond',

        symbolSize: 9,

        showSymbol: true,

        lineStyle: {
          width: 2.5,

          color: '#2A9D8F'
        },

        itemStyle: {
          color: '#2A9D8F'
        },

        emphasis: {
          focus: 'series',

          lineStyle: {
            width: 4
          },

          symbolSize: 12
        }
      },

      {
        name: 'Dynamic Accuracy',

        type: 'line',

        data: toNormalized(dynamic),

        smooth: false,

        symbol: 'triangle',

        symbolSize: 10,

        showSymbol: true,

        lineStyle: {
          width: 2.5,

          color: '#20639B'
        },

        itemStyle: {
          color: '#20639B'
        },

        emphasis: {
          focus: 'series',

          lineStyle: {
            width: 4
          },

          symbolSize: 13
        }
      },

      {
        name: 'Structural Accuracy',

        type: 'line',

        data: toNormalized(structural),

        smooth: false,

        symbol: 'rect',

        symbolSize: 8,

        showSymbol: true,

        lineStyle: {
          width: 2.5,

          color: '#7A5AF8'
        },

        itemStyle: {
          color: '#7A5AF8'
        },

        emphasis: {
          focus: 'series',

          lineStyle: {
            width: 4
          },

          symbolSize: 11
        }
      }
    ]
  }

  chart.setOption(option)
}

function handleResize() {
  chart?.resize()
}

onMounted(() => {
  createChart()

  window.addEventListener(
    'resize',
    handleResize
  )
})

onBeforeUnmount(() => {
  window.removeEventListener(
    'resize',
    handleResize
  )

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

.chart-kicker {
  font-family: 'IBM Plex Mono', monospace;

  font-size: 10px;

  font-weight: 600;

  letter-spacing: 0.12em;

  color: #20639B;

  margin-bottom: 5px;
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

  min-height: 0;

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