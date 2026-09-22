<script setup>

import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import * as echarts from 'echarts'

const performanceChartRef = ref(null)
const timeChartRef = ref(null)

let performanceChart = null
let timeChart = null
let resizeObserver = null


/* ============================================================
 * DATA
 * ============================================================ */

const networkSizes = ['10', '50', '100']

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


/* ============================================================
 * PERFORMANCE ERROR BARS
 *
 * Error bars are calculated from the SAME bar geometry used
 * by renderItem().
 *
 * This avoids using getBoundingRect() on the group, because
 * the group contains both the bar and the rotated text label.
 * ============================================================ */

/* ============================================================
 * PERFORMANCE ERROR BARS
 *
 * Error bars are rendered directly with ZRender instead of
 * ECharts graphic/setOption.
 *
 * This avoids graphic merge conflicts and keeps the legend
 * completely independent from the error-bar layer.
 * ============================================================ */

let errorBarGroup = null

function renderErrorBars() {

  if (!performanceChart) return

  const zr = performanceChart.getZr()

  if (!zr) return


  /* ----------------------------------------------------------
   * Remove previous error-bar layer
   * ---------------------------------------------------------- */

  if (errorBarGroup) {

    zr.remove(errorBarGroup)

    errorBarGroup = null

  }


  /* ----------------------------------------------------------
   * Create a new ZRender group
   * ---------------------------------------------------------- */

  errorBarGroup =
    new echarts.graphic.Group()


  /*
   * These values MUST match the custom bar geometry.
   */

  const BAR_WIDTH = 22
  const BAR_GAP = 0


  /*
   * Get ECharts series data.
   */

  const seriesModel = performanceChart
    .getModel()
    .getSeriesByIndex(0)

  if (!seriesModel) return

  const data = seriesModel.getData()

  if (!data) return


  /*
   * ----------------------------------------------------------
   * Iterate through every actual rendered bar.
   * ----------------------------------------------------------
   */

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


    /*
     * Skip missing values.
     */

    if (
      mean === null ||
      std === null ||
      mean === undefined ||
      std === undefined
    ) {
      continue
    }


    /*
     * --------------------------------------------------------
     * Calculate EXACT center of the bar.
     *
     * This is identical to renderItem().
     * --------------------------------------------------------
     */

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


    /*
     * --------------------------------------------------------
     * Convert mean ± std into pixel coordinates.
     * --------------------------------------------------------
     */

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


    /*
     * Width of horizontal caps.
     */

    const capWidth =
      Math.min(
        BAR_WIDTH * 0.4,
        6
      )


    /*
     * --------------------------------------------------------
     * Vertical STD line
     * --------------------------------------------------------
     */

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


    /*
     * --------------------------------------------------------
     * Upper cap
     * --------------------------------------------------------
     */

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


    /*
     * --------------------------------------------------------
     * Lower cap
     * --------------------------------------------------------
     */

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


    /*
     * Add all three elements to the error-bar group.
     */

    errorBarGroup.add(verticalLine)

    errorBarGroup.add(upperCap)

    errorBarGroup.add(lowerCap)

  }


  /*
   * ----------------------------------------------------------
   * Add the complete error-bar layer to ZRender.
   * ----------------------------------------------------------
   */

  zr.add(errorBarGroup)


  /*
   * Make sure error bars stay above the bars.
   */

  errorBarGroup.z = 100

}


/* ============================================================
 * PERFORMANCE CHART
 * ============================================================ */

function createPerformanceOption() {

  const names = Object.keys(performanceData)


  /*
   * Actual number of bars in each group.
   *
   * |V| = 10  -> 3 bars
   * |V| = 50  -> 4 bars
   * |V| = 100 -> 4 bars
   */

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


  /*
   * Fixed physical bar width.
   */

  const BAR_WIDTH = 22


  /*
   * Bars touch each other.
   */

  const BAR_GAP = 0


  /*
   * One custom series renders all actual bars.
   *
   * This prevents ECharts from reserving empty slots
   * for null values.
   */

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


        /*
         * Determine the position of this actual bar
         * among the bars that REALLY exist in this group.
         */

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


    /*
     * ----------------------------------------------------------
     * GRID
     *
     * Reduced top spacing so the legend is close to the chart.
     * ----------------------------------------------------------
     */

    grid: {
      left: 48,
      right: 18,

      top: 54,

      bottom: 52,

      containLabel: true
    },


    /*
     * ----------------------------------------------------------
     * LEGEND + ERROR BAR GRAPHIC GROUPS
     * ----------------------------------------------------------
     */

    graphic: [

      /*
       * --------------------------------------------------------
       * LEGEND
       *
       * It is now BELOW "(a)".
       * --------------------------------------------------------
       */

      {
        id: 'performance-legend',

        type: 'group',

        left: 'center',

        top: 24,

        children: [

          /* 5 000 */

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


          /* 10 000 */

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


          /* 20 000 */

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


          /* 2 000 (|V|=50) */

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


          /* 2 000 (|V|=100) */

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
      },


      /*
       * --------------------------------------------------------
       * ERROR BAR GROUP
       *
       * Initially empty.
       * renderErrorBars() fills this group after ECharts
       * calculates the actual chart coordinates.
       * --------------------------------------------------------
       */

    ],


    /*
     * ----------------------------------------------------------
     * TITLE
     * ----------------------------------------------------------
     */

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


    /*
     * ----------------------------------------------------------
     * X AXIS
     * ----------------------------------------------------------
     */

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


    /*
     * ----------------------------------------------------------
     * Y AXIS
     * ----------------------------------------------------------
     */

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


    /*
     * ----------------------------------------------------------
     * TOOLTIP
     * ----------------------------------------------------------
     */

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


    /*
     * ========================================================
     * ONE CUSTOM BAR SERIES
     * ========================================================
     */

    series: [

      {

        name: 'Performance',

        type: 'custom',

        data: barData,


        /*
         * ------------------------------------------------------
         * CUSTOM BAR RENDERING
         * ------------------------------------------------------
         */

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


          /*
           * Category center.
           */

          const categoryCenter =
            api.coord([
              categoryIndex,
              0
            ])[0]


          /*
           * Total width of all bars in this category.
           */

          const groupWidth =
            barCount * BAR_WIDTH +
            (barCount - 1) * BAR_GAP


          /*
           * Left edge of the group.
           */

          const groupLeft =
            categoryCenter -
            groupWidth / 2


          /*
           * Center of this specific bar.
           */

          const centerX =
            groupLeft +
            barIndex *
              (BAR_WIDTH + BAR_GAP) +
            BAR_WIDTH / 2


          /*
           * Vertical coordinates.
           */

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

              /*
               * Bar
               */

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


              /*
               * Data label
               */

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


        /*
         * Keep tooltip controlled manually.
         */

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


  /*
   * Dispose existing charts.
   */

  if (performanceChart) {

    performanceChart.dispose()

    performanceChart = null

  }

  if (timeChart) {

    timeChart.dispose()

    timeChart = null

  }


  /*
   * Create performance chart.
   */

  performanceChart =
    echarts.init(
      performanceChartRef.value,
      null,
      {
        renderer: 'svg'
      }
    )


  /*
   * Create training-time chart.
   */

  timeChart =
    echarts.init(
      timeChartRef.value,
      null,
      {
        renderer: 'svg'
      }
    )


  /*
   * ----------------------------------------------------------
   * 1. Render performance BAR chart first.
   * ----------------------------------------------------------
   */

  performanceChart.setOption(
    createPerformanceOption()
  )


  /*
   * ----------------------------------------------------------
   * 2. Force ECharts to calculate the actual layout.
   * ----------------------------------------------------------
   */

  performanceChart.resize()


  /*
   * ----------------------------------------------------------
   * 3. Render error bars only AFTER the chart layout exists.
   *
   * Two animation frames ensure that ECharts has completed
   * its SVG layout before error-bar coordinates are calculated.
   * ----------------------------------------------------------
   */

//   requestAnimationFrame(() => {

//     requestAnimationFrame(() => {

//       //renderErrorBars()

//     })

//   })


  /*
   * ----------------------------------------------------------
   * Render training-time chart.
   * ----------------------------------------------------------
   */

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


      /*
       * The real bar positions change after resize.
       * Therefore error bars must be regenerated.
       */

    //   requestAnimationFrame(() => {

    //     renderErrorBars()

    //   })

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

})


/* ============================================================
 * UNMOUNT
 * ============================================================ */

onBeforeUnmount(() => {

  window.removeEventListener(
    'resize',
    resizeCharts
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

    <div class="charts-row">

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


    <div class="result-note">
        <div class="result-item">
            <span class="note-icon">▸</span>
            <div>
                <strong>Cross-size generalization: </strong>
                GNB trained solely on |V|=10 networks achieves 0.373 AUPR on |V|=50 and 0.333 on |V|=100.
            </div>
        </div>

        <div class="result-item">
            <span class="note-icon">▸</span>
            <div>
                <strong>Competitive predictive power: </strong>
                Matches or exceeds direct training on target-size networks (0.359 on |V|=50; 0.326 on |V|=100).
            </div>
        </div>

        <div class="result-item">
            <span class="note-icon">▸</span>
            <div>
                <strong>Empirical validation: </strong>
                Confirms true scale-invariant knowledge transfer across network dimensions.
            </div>
        </div>
    </div>

  </div>

</template>


<style scoped>

.gwn-training-size {
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
 *
 * Chart (a) gets slightly more width because it contains
 * the legend and five grouped bars.
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

  /*
   * Leave explicit space for the result note.
   */
  padding-bottom: 2px;
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
 * RESULT NOTE
 * ============================================================
 */

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

  .gwn-training-size {
    padding-left: 2px;
    padding-right: 2px;
  }

}

</style>