<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const chartRef = ref(null)
let chart = null
let resizeObserver = null

// ============================================================
// Data — directly from the Python experiment
// ============================================================

const networkSizes = ['10', '50', '100']

const performanceData = {
  '10 time steps': [0.71, 0.28, 0.23],
  '20 time steps': [0.69, 0.35, 0.29],
  '50 time steps': [0.57, 0.36, 0.32]
}

const seriesColors = {
  '10 time steps': '#66C2A5',
  '20 time steps': '#FC8D62',
  '50 time steps': '#8DA0CB'
}

// ============================================================
// Chart option
// ============================================================

function createChartOption() {
  return {
    animation: false,

    grid: {
      left: 58,
      right: 24,
      top: 62,
      bottom: 58,
      containLabel: true
    },

    legend: {
      top: 2,
      left: 'center',
      itemWidth: 16,
      itemHeight: 10,
      itemGap: 18,
      textStyle: {
        fontSize: 11,
        color: '#24313A'
      }
    },

    xAxis: {
      type: 'category',
      data: networkSizes,
      name: 'Network Size of Test Set',
      nameLocation: 'middle',
      nameGap: 34,
      nameTextStyle: {
        fontSize: 12,
        color: '#24313A'
      },
      axisLine: {
        lineStyle: {
          color: '#717375'
        }
      },
      axisTick: {
        alignWithLabel: true
      },
      axisLabel: {
        fontSize: 11,
        color: '#24313A'
      }
    },

    yAxis: {
      type: 'value',
      min: 0,
      max: 1,
      interval: 0.2,
      name: 'Performance',
      nameLocation: 'middle',
      nameGap: 42,
      nameTextStyle: {
        fontSize: 12,
        color: '#24313A'
      },
      axisLine: {
        show: false
      },
      axisTick: {
        show: false
      },
      axisLabel: {
        fontSize: 10,
        color: '#24313A'
      },
      splitLine: {
        show: true,
        lineStyle: {
          color: '#DCE4E9',
          type: 'dashed',
          opacity: 0.8
        }
      }
    },

    tooltip: {
      trigger: 'axis',
      axisPointer: {
        type: 'shadow'
      },
      formatter(params) {
        if (!params || !params.length) return ''

        let html = `
          <div style="font-weight:600;margin-bottom:6px;">
            Network Size: ${params[0].axisValue}
          </div>
        `

        params.forEach(item => {
          html += `
            <div style="display:flex;justify-content:space-between;gap:18px;">
              <span>${item.marker}${item.seriesName}</span>
              <strong>${Number(item.value).toFixed(2)}</strong>
            </div>
          `
        })

        return html
      }
    },

    series: Object.entries(performanceData).map(([name, values]) => ({
      name,
      type: 'bar',
      data: values,
      barWidth: 22,
      barGap: '0%',
      barCategoryGap: '25%',

      itemStyle: {
        color: seriesColors[name],
        borderColor: '#717375',
        borderWidth: 1
      },

      label: {
        show: true,
        position: 'top',
        distance: 4,
        fontSize: 10,
        color: '#24313A',
        formatter: params => Number(params.value).toFixed(2)
      },

      emphasis: {
        itemStyle: {
          opacity: 0.9
        }
      }
    }))
  }
}

// ============================================================
// Resize
// ============================================================

let resizeRaf = null

function resizeChart() {
  if (resizeRaf) {
    cancelAnimationFrame(resizeRaf)
  }

  resizeRaf = requestAnimationFrame(() => {
    resizeRaf = null

    if (chart) {
      chart.resize()
    }
  })
}

// ============================================================
// Lifecycle
// ============================================================

onMounted(async () => {
  await nextTick()

  if (!chartRef.value) return

  chart = echarts.init(chartRef.value, null, {
    renderer: 'svg'
  })

  chart.setOption(createChartOption())

  resizeObserver = new ResizeObserver(() => {
    resizeChart()
  })

  resizeObserver.observe(chartRef.value)

  window.addEventListener('resize', resizeChart)
})

onBeforeUnmount(() => {
  if (resizeRaf) {
    cancelAnimationFrame(resizeRaf)
    resizeRaf = null
  }

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
  <div class="few-time-steps">
    <div class="chart-panel">
      <div ref="chartRef" class="chart"></div>
    </div>

    <div class="insight-panel">
      <div class="insight-label">
        EXPERIMENT
      </div>

      <h3>
        Limited temporal observations
      </h3>

      <div class="experiment-list">
        <div class="experiment-item">
          <span class="dot"></span>
          <div>
            <strong>Network sizes</strong>
            <span>10, 50, and 100 genes</span>
          </div>
        </div>

        <div class="experiment-item">
          <span class="dot"></span>
          <div>
            <strong>Time steps</strong>
            <span>10, 20, and 50</span>
          </div>
        </div>

        <div class="experiment-item">
          <span class="dot"></span>
          <div>
            <strong>Objective</strong>
            <span>
              Evaluate performance under limited temporal observations
            </span>
          </div>
        </div>
      </div>

      <div class="finding">
        <div class="finding-label">
          KEY FINDING
        </div>

        <p>
          The model remains effective even with
          <strong>only 10 time steps</strong>,
          supporting its applicability to more realistic
          temporal sampling conditions.
        </p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.few-time-steps {
  width: 100%;
  height: 100%;
  display: grid;
  grid-template-columns: minmax(0, 1.65fr) minmax(220px, 0.75fr);
  gap: 24px;
  box-sizing: border-box;
  margin-top: 20px;
}

.chart-panel {
  min-width: 0;
  min-height: 0;
  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 10px;
  padding: 8px 10px 4px;
  box-sizing: border-box;
}

.chart {
  width: 100%;
  height: 100%;
  min-height: 280px;
}

.insight-panel {
  min-width: 0;
  display: flex;
  flex-direction: column;
  padding: 8px 4px 8px 4px;
}

.insight-label {
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: #20639b;
  margin-bottom: 8px;
}

.insight-panel h3 {
  margin: 0 0 18px;
  font-size: 18px;
  line-height: 1.25;
  font-weight: 700;
  color: #173f5f;
}

.experiment-list {
  display: flex;
  flex-direction: column;
  gap: 13px;
}

.experiment-item {
  display: flex;
  align-items: flex-start;
  gap: 9px;
  font-size: 12px;
  line-height: 1.35;
  color: #64748b;
}

.experiment-item .dot {
  width: 7px;
  height: 7px;
  margin-top: 5px;
  flex: 0 0 7px;
  border-radius: 50%;
  background: #2a9d8f;
}

.experiment-item strong {
  display: block;
  margin-bottom: 2px;
  color: #24313a;
  font-size: 12px;
}

.experiment-item span:not(.dot) {
  display: block;
}

.finding {
  margin-top: auto;
  padding: 14px 15px;
  background: #f8fafb;
  border-left: 3px solid #2a9d8f;
  border-radius: 0 7px 7px 0;
}

.finding-label {
  margin-bottom: 7px;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.1em;
  color: #2a9d8f;
}

.finding p {
  margin: 0;
  font-size: 12px;
  line-height: 1.45;
  color: #24313a;
}

.finding strong {
  color: #173f5f;
}

@media (max-width: 760px) {
  .few-time-steps {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .insight-panel {
    padding-top: 0;
  }

  .finding {
    margin-top: 12px;
  }
}
</style>