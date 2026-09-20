<template>
  <div class="results-slide">
    <div class="chart-header">
      <div>
        <div class="chart-description">
          Performance remains strong across structural and dynamic evaluation metrics.
        </div>
      </div>

      <div class="dataset-badge">
        <span>20 network sizes</span>
        <span class="dot">·</span>
        <span>10–200 genes</span>
      </div>
    </div>

    <div ref="chartRef" class="chart"></div>

    <div class="bottom-message">
      <span class="message-mark"></span>
      <span>
        Strong structural and dynamic performance demonstrates the potential of the proposed method for GRN inference.
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)

let chart = null

const networkSize = [
  10, 20, 30, 40, 50,
  60, 70, 80, 90, 100,
  110, 120, 130, 140, 150,
  160, 170, 180, 190, 200
]

const precision = [
  79, 67, 65, 59, 58,
  57, 54, 56, 53, 52,
  52, 51, 51, 48, 50,
  48, 47, 50, 50, 49
]

const recall = [
  79, 74, 70, 66, 65,
  63, 60, 63, 60, 58,
  59, 57, 57, 54, 56,
  54, 52, 55, 54, 54
]

const dynamicAccuracy = [
  100, 100, 100, 100, 100,
  100, 100, 100, 100, 100,
  100, 100, 100, 100, 100,
  100, 100, 100, 100, 100
]

const structuralAccuracy = [
  91, 93, 95, 96, 97,
  97, 97, 98, 98, 98,
  98, 98, 99, 98, 99,
  99, 99, 99, 99, 99
]

const toNormalized = values =>
  values.map(value => value / 100)

function createChart() {
  if (!chartRef.value) return

 // chart = echarts.init(chartRef.value)
   const chart = echarts.init(chartRef.value, null, {
  renderer: 'svg'
})

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
      if (!params || !params.length) return ''

      const network = params[0].axisValue

      let html = `
        <div style="font-weight:600;margin-bottom:7px;">
          Network size: ${network} genes
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
              ${(value).toFixed(0)}
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

    data: networkSize,

    name: 'Network size (genes)',
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
      fontSize: 10,

      // Show EVERY value: 10, 20, ..., 200
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

    // Updated Y-axis range
    min: 0.4,
    max: 1.0,
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

      // Circle marker
      symbol: 'circle',
      symbolSize: 7,
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

        symbolSize: 10
      }
    },

    {
      name: 'Recall',
      type: 'line',

      data: toNormalized(recall),

      smooth: false,

      // Diamond marker
      symbol: 'diamond',
      symbolSize: 8,
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

        symbolSize: 11
      }
    },

    {
      name: 'Dynamic Accuracy',
      type: 'line',

      data: toNormalized(dynamicAccuracy),

      smooth: false,

      // Triangle marker
      symbol: 'triangle',
      symbolSize: 9,
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

        symbolSize: 12
      }
    },

    {
      name: 'Structural Accuracy',
      type: 'line',

      data: toNormalized(structuralAccuracy),

      smooth: false,

      // Square marker
      symbol: 'rect',
      symbolSize: 7,
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

        symbolSize: 10
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
  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)

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