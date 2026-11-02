<script setup>

import { ref, computed, onMounted, onBeforeUnmount, nextTick, watch } from 'vue'
import * as echarts from 'echarts'
import { useNav } from '@slidev/client'

const performanceChartRef = ref(null)
const timeChartRef = ref(null)

let performanceChart = null
let timeChart = null
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

const networkSizes = ['10', '50', '100']
//const networkSizes = ['10', '50', '100']

const performanceData = {
  '5 000': [
    { mean: 0.5727, std: 0.1743 },
    { mean: 0.3487, std: 0.074 },
    { mean: 0.3224, std: 0.0473 }
  ],

  '10 000': [
    { mean: 0.5785, std: 0.1763 },
    { mean: 0.3518, std: 0.076 },
    { mean: 0.3249, std: 0.049 }
  ],

  '20 000': [
    { mean: 0.674, std: 0.1641 },
    { mean: 0.3729, std: 0.078 },
    { mean: 0.3334, std: 0.028 }
  ],

  '2 000 (|V|=50)': [
    { mean: null, std: null },
    { mean: 0.3594, std: 0.072 },
    { mean: null, std: null }
  ],

  '2 000 (|V|=100)': [
    { mean: null, std: null },
    { mean: null, std: null },
    { mean: 0.326, std: 0.026 }
  ]
}

/* ============================================================
 * EXACT COLORS CORRESPONDING TO EACH BAR SERIES
 * ============================================================ */

const seriesColors = {
  '5 000': '#66C2A5',
  '10 000': '#FC8D62',
  '20 000': '#8DA0CB',
  '2 000 (|V|=50)': '#E78AC3',
  '2 000 (|V|=100)': '#E5C494'
}


/* ============================================================
 * TRAINING TIME
 * ============================================================ */

const trainingTime = [
  {
    name: '5 000',
    value: 2.58,
    color: '#66C2A5',
    hatch: false
  },
  {
    name: '10 000',
    value: 2.86,
    color: '#FC8D62',
    hatch: false
  },
  {
    name: '20 000',
    value: 3.21,
    color: '#8DA0CB',
    hatch: false
  },
  {
    name: '2 000 (|V|=50)',
    value: 3.79,
    color: '#E78AC3',
    hatch: false
  },
  {
    name: '2 000 (|V|=100)',
    value: 4.27,
    color: '#E5C494',
    hatch: false
  }
]


let errorBarGroup = null

function renderErrorBars() {

  if (!performanceChart) return

  const zr = performanceChart.getZr()

  if (!zr) return

  if (errorBarGroup) {

    zr.remove(errorBarGroup)

    errorBarGroup = null

  }

  errorBarGroup =
    new echarts.graphic.Group()

  const BAR_WIDTH = 22
  const BAR_GAP = 0

  const seriesModel = performanceChart
    .getModel()
    .getSeriesByIndex(0)

  if (!seriesModel) return

  const data = seriesModel.getData()

  if (!data) return

  for (
    let dataIndex = 0;
    dataIndex < data.count();
    dataIndex++
  ) {

    const rawData =
      data.getRawDataItem(dataIndex)

    if (!rawData) continue

    const categoryIndex =
      rawData.categoryIndex

    const mean =
      rawData.mean

    const std =
      rawData.std

    const barIndex =
      rawData.barIndex

    const barCount =
      rawData.barCount

    if (
      mean === null ||
      std === null ||
      mean === undefined ||
      std === undefined
    ) {
      continue
    }

    const categoryCenter =
      performanceChart.convertToPixel(
        { seriesIndex: 0 },
        [categoryIndex, 0]
      )[0]

    const groupWidth =
      barCount * BAR_WIDTH +
      (barCount - 1) * BAR_GAP

    const groupLeft =
      categoryCenter -
      groupWidth / 2

    const centerX =
      groupLeft +
      barIndex *
        (BAR_WIDTH + BAR_GAP) +
      BAR_WIDTH / 2

    const upper =
      performanceChart.convertToPixel(
        { seriesIndex: 0 },
        [
          categoryIndex,
          Math.min(1, mean + std)
        ]
      )

    const lower =
      performanceChart.convertToPixel(
        { seriesIndex: 0 },
        [
          categoryIndex,
          Math.max(0, mean - std)
        ]
      )

    const yUpper = upper[1]
    const yLower = lower[1]

    const capWidth =
      Math.min(
        BAR_WIDTH * 0.4,
        6
      )

    const verticalLine =
      new echarts.graphic.Line({

        shape: {

          x1: centerX,
          y1: yUpper,

          x2: centerX,
          y2: yLower

        },

        style: {

          stroke: '#eb5f34',

          lineWidth: 1.5

        },

        silent: true

      })

    const upperCap =
      new echarts.graphic.Line({

        shape: {

          x1:
            centerX -
            capWidth,

          y1: yUpper,

          x2:
            centerX +
            capWidth,

          y2: yUpper

        },

        style: {

          stroke: '#eb5f34',

          lineWidth: 1.5

        },

        silent: true

      })

    const lowerCap =
      new echarts.graphic.Line({

        shape: {

          x1:
            centerX -
            capWidth,

          y1: yLower,

          x2:
            centerX +
            capWidth,

          y2: yLower

        },

        style: {

          stroke: '#eb5f34',

          lineWidth: 1.5

        },

        silent: true

      })

    errorBarGroup.add(verticalLine)

    errorBarGroup.add(upperCap)

    errorBarGroup.add(lowerCap)

  }

  zr.add(errorBarGroup)

  errorBarGroup.z = 100

}


/* ============================================================
 * PERFORMANCE CHART
 * ============================================================ */

function createPerformanceOption() {

  const names = Object.keys(performanceData)

  const groupBarCount = performanceData['5 000'].map(
    (_, categoryIndex) => {

      return names.reduce(
        (count, name) => {

          const item =
            performanceData[name][categoryIndex]

          return count + (
            item &&
            item.mean !== null
              ? 1
              : 0
          )

        },
        0
      )

    }
  )

  const BAR_WIDTH = 22

  const BAR_GAP = 0

  const barData = []

  names.forEach((name, seriesIndex) => {

    performanceData[name].forEach(
      (item, categoryIndex) => {

        if (
          !item ||
          item.mean === null
        ) {
          return
        }

        let barIndex = 0

        for (
          let i = 0;
          i < seriesIndex;
          i++
        ) {

          const previousItem =
            performanceData[names[i]][categoryIndex]

          if (
            previousItem &&
            previousItem.mean !== null
          ) {
            barIndex++
          }

        }

        barData.push({

          value: [
            categoryIndex,
            item.mean
          ],

          categoryIndex,

          seriesIndex,

          name,

          mean: item.mean,

          std: item.std,

          barIndex,

          barCount:
            groupBarCount[categoryIndex]

        })

      }
    )

  })


  return {

    animation: false,

    grid: {
      left: 48,
      right: 18,

      top: 54,

      bottom: 52,

      containLabel: true
    },

    graphic: [

      {
        id: 'performance-legend',

        type: 'group',

        left: 'center',

        top: 24,

        children: [

          {
            type: 'rect',

            shape: {
              x: 0,
              y: 2,

              width: 15,
              height: 8
            },

            style: {
              fill: seriesColors['5 000']
            }
          },

          {
            type: 'text',

            style: {
              x: 17,
              y: 2,

              text: '5 000',

              fill: '#334155',

              fontSize: 11
            }
          },

          {
            type: 'rect',

            shape: {
              x: 70,
              y: 2,

              width: 15,
              height: 8
            },

            style: {
              fill: seriesColors['10 000']
            }
          },

          {
            type: 'text',

            style: {
              x: 87,
              y: 2,

              text: '10 000',

              fill: '#334155',

              fontSize: 11
            }
          },

          {
            type: 'rect',

            shape: {
              x: 145,
              y: 2,

              width: 15,
              height: 8
            },

            style: {
              fill: seriesColors['20 000']
            }
          },

          {
            type: 'text',

            style: {
              x: 162,
              y: 2,

              text: '20 000',

              fill: '#334155',

              fontSize: 11
            }
          },

          {
            type: 'rect',

            shape: {
              x: 225,
              y: 2,

              width: 15,
              height: 8
            },

            style: {
              fill: seriesColors['2 000 (|V|=50)']
            }
          },

          {
            type: 'text',

            style: {
              x: 242,
              y: 0,

              text: '2 000 (|V|=50)',

              fill: '#334155',

              fontSize: 11
            }
          },

          {
            type: 'rect',

            shape: {
              x: 360,
              y: 2,

              width: 15,
              height: 8
            },

            style: {
              fill: seriesColors['2 000 (|V|=100)']
            }
          },

          {
            type: 'text',

            style: {
              x: 377,
              y: 2,

              text: '2 000 (|V|=100)',

              fill: '#334155',

              fontSize: 11
            }
          }

        ]
      }

    ],

    title: {

      text: '(a)',

      left: 'center',

      top: 2,

      textStyle: {
        fontSize: 14,

        fontWeight: 600,

        color: '#24313A'
      }

    },

    xAxis: {

      type: 'category',

      data: networkSizes,

      name: 'Network Size of Test Set',

      nameLocation: 'middle',

      nameGap: 34,

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

      },

      nameTextStyle: {

        color: '#475569',

        fontSize: 9

      }

    },

    yAxis: {

      type: 'value',

      min: 0,

      max: 1,

      interval: 0.2,

      name: 'Performance',

      nameLocation: 'middle',

      nameGap: 32,

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

        const categoryIndex =
          params[0]?.dataIndex

        if (
          categoryIndex === undefined ||
          categoryIndex === null
        ) {
          return ''
        }

        const lines = []

        names.forEach(name => {

          const value =
            performanceData[name]?.[categoryIndex]

          if (
            !value ||
            value.mean === null
          ) {
            return
          }

          lines.push(

            `<span style="
              display:inline-block;
              width:8px;
              height:8px;
              border-radius:50%;
              background:${seriesColors[name]};
              margin-right:6px;
            "></span>` +

            `${name}: ${value.mean.toFixed(3)} ± ${value.std.toFixed(2)}`
          )

        })

        return `
          <div style="font-size:12px;line-height:1.6">
            <strong>|V| = ${networkSizes[categoryIndex]}</strong>
            <br/>
            ${lines.join('<br/>')}
          </div>
        `

      }

    },

    series: [

      {

        name: 'Performance',

        type: 'custom',

        data: barData,

        renderItem(params, api) {

          const item =
            barData[params.dataIndex]

          if (!item) return null

          const categoryIndex =
            item.categoryIndex

          const mean =
            item.mean

          const barIndex =
            item.barIndex

          const barCount =
            item.barCount

          const categoryCenter =
            api.coord([
              categoryIndex,
              0
            ])[0]

          const groupWidth =
            barCount * BAR_WIDTH +
            (barCount - 1) * BAR_GAP

          const groupLeft =
            categoryCenter -
            groupWidth / 2

          const centerX =
            groupLeft +
            barIndex *
              (BAR_WIDTH + BAR_GAP) +
            BAR_WIDTH / 2

          const yZero =
            api.coord([
              categoryIndex,
              0
            ])[1]

          const yValue =
            api.coord([
              categoryIndex,
              mean
            ])[1]

          const height =
            yZero - yValue

          return {

            type: 'group',

            children: [

              {
                type: 'rect',

                shape: {

                  x:
                    centerX -
                    BAR_WIDTH / 2,

                  y: yValue,

                  width: BAR_WIDTH,

                  height

                },

                style: {

                  fill:
                    seriesColors[item.name],

                  stroke: 'none'

                }

              },

              {

                type: 'text',

                style: {

                  text:
                    mean.toFixed(3),

                  x: centerX,

                  y:
                    yValue +
                    height / 2,

                  fill: '#000',

                  fontSize: 9,

                  fontWeight: 500,

                  textAlign: 'center',

                  textVerticalAlign:
                    'middle'

                },

                rotation:
                  -Math.PI / 2,

                originX: centerX,

                originY:
                  yValue +
                  height / 2

              }

            ]

          }

        },

        encode: {

          x: 0,

          y: 1

        },

        z: 2

      }

    ]

  }

}


/* ============================================================
 * TRAINING TIME CHART
 * ============================================================ */

function createTimeOption() {

  return {

    animation: false,

    grid: {

      left: 58,

      right: 18,

      top: 32,

      bottom: 38,

      containLabel: true

    },

    title: {

      text: '(b)',

      left: 'center',

      top: 2,

      textStyle: {

        fontSize: 14,

        fontWeight: 600,

        color: '#24313A'

      }

    },

    xAxis: {

      type: 'category',

      data:
        trainingTime.map(
          item => item.name
        ),

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

        show: false

      }

    },

    yAxis: {

      type: 'value',

      min: 0,

      max: 5,

      interval: 1,

      name: 'Training time [log₁₀(ms)]',

      nameLocation: 'middle',

      nameGap: 40,

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

        formatter:
          value =>
            value.toFixed(0)

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

        const index =
          params[0]?.dataIndex

        if (index === undefined) {
          return ''
        }

        const item =
          trainingTime[index]

        return `
          <div style="font-size:12px;line-height:1.6">
            <strong>${item.name}</strong><br/>
            Training time: ${item.value.toFixed(2)}
          </div>
        `

      }

    },

    series: [

      {

        type: 'bar',

        data:
          trainingTime.map(
            item => ({

              value: item.value,

              itemStyle: {

                color: item.color,

                borderWidth: 0,

                decal:
                  item.hatch
                    ? {

                        symbol: 'rect',

                        symbolSize: 1,

                        color:
                          'rgba(113,115,117,0.45)',

                        dashArrayX: [1, 0],

                        dashArrayY: [1, 4],

                        rotation:
                          Math.PI / 4

                      }
                    : undefined

              }

            })
          ),

        label: {

          show: true,

          position: 'top',

          distance: 5,

          formatter: params =>
            params.value.toFixed(2),

          color: '#000',

          fontSize: 10,

          fontWeight: 500

        },

        barMaxWidth: 34

      }

    ]

  }

}


/* ============================================================
 * INITIALIZATION
 * ============================================================ */

async function initCharts() {

  await nextTick()

  if (
    !performanceChartRef.value ||
    !timeChartRef.value
  ) {
    return
  }

  if (performanceChart) {

    performanceChart.dispose()

    performanceChart = null

  }

  if (timeChart) {

    timeChart.dispose()

    timeChart = null

  }

  performanceChart =
    echarts.init(
      performanceChartRef.value,
      null,
      {
        renderer: 'svg'
      }
    )

  timeChart =
    echarts.init(
      timeChartRef.value,
      null,
      {
        renderer: 'svg'
      }
    )

  performanceChart.setOption(
    createPerformanceOption()
  )

  performanceChart.resize()

  timeChart.setOption(
    createTimeOption()
  )

  timeChart.resize()

}


/* ============================================================
 * RESIZE
 * ============================================================ */

function resizeCharts() {

  requestAnimationFrame(() => {

    if (performanceChart) {

      performanceChart.resize()

    }

    if (timeChart) {

      timeChart.resize()

    }

  })

}


/* ============================================================
 * MOUNT
 * ============================================================ */

onMounted(async () => {

  await initCharts()

  resizeObserver =
    new ResizeObserver(() => {

      resizeCharts()

    })

  if (performanceChartRef.value) {

    resizeObserver.observe(
      performanceChartRef.value
    )

  }

  if (timeChartRef.value) {

    resizeObserver.observe(
      timeChartRef.value
    )

  }

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


/* ============================================================
 * UNMOUNT
 * ============================================================ */

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

    resizeObserver = null

  }

  if (performanceChart) {

    if (errorBarGroup) {

      performanceChart
        .getZr()
        .remove(errorBarGroup)

      errorBarGroup = null

    }

    performanceChart.dispose()

    performanceChart = null

  }

  if (timeChart) {

    timeChart.dispose()

    timeChart = null

  }

})

</script>


<template>

  <div class="gwn-training-size">

    <div class="charts-row" :class="{ 'note-open': notesVisible }">

      <div class="chart-card">
        <div
          ref="performanceChartRef"
          class="chart"
        ></div>
      </div>

      <div class="chart-card">
        <div
          ref="timeChartRef"
          class="chart"
        ></div>
      </div>

    </div>


    <div v-if="notesVisible" class="findings">

      <Transition name="card-pop">
        <div v-if="visibleCount >= 1" class="finding">
          <div class="finding-header">
            <span class="finding-number">01</span>
            <h3>Cross-size generalization</h3>
          </div>
          <p>
            GNB trained solely on |V|=10 networks achieves 0.373 AUPR on |V|=50 and 0.333 on |V|=100.
          </p>
        </div>
      </Transition>

      <Transition name="card-pop">
        <div v-if="visibleCount >= 2" class="finding">
          <div class="finding-header">
            <span class="finding-number">02</span>
            <h3>Competitive predictive power</h3>
          </div>
          <p>
            Matches or exceeds direct training on target-size networks (0.359 on |V|=50; 0.326 on |V|=100).
          </p>
        </div>
      </Transition>

      <Transition name="card-pop">
        <div v-if="visibleCount >= 3" class="finding">
          <div class="finding-header">
            <span class="finding-number">03</span>
            <h3>Empirical validation</h3>
          </div>
          <p>
            Confirms true scale-invariant knowledge transfer across network dimensions.
          </p>
        </div>
      </Transition>

    </div>

  </div>

</template>


<style scoped>

.gwn-training-size {
  position: relative;

  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 4px 6px 0;
}


/*
 * Two charts in one row.
 * Takes the FULL height by default (notes hidden); shrinks
 * only once the first finding card is revealed.
 */
.charts-row {
  flex: 1;

  min-height: 0;

  display: grid;

  grid-template-columns:
    minmax(0, 1.25fr)
    minmax(0, 1fr);

  gap: 8px;

  width: 100%;

  padding-bottom: 2px;

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


/*
 * ============================================================
 * FINDINGS — horizontal row of cards, revealed one at a time
 * via SPACE, same style as the "findings" grid used elsewhere
 * in the deck
 * ============================================================
 */

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


/*
 * ============================================================
 * RESPONSIVE
 * ============================================================
 */

@media (max-width: 900px) {

  .charts-row {
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr;

    gap: 4px;
  }

  .findings {
    grid-template-columns: 1fr;
  }

  .gwn-training-size {
    padding-left: 2px;
    padding-right: 2px;
  }

}

</style>