<template>
  <canvas ref="radarCanvas" />
</template>

<script setup>
  import { Chart, Legend, LineElement, PointElement, RadarController, RadialLinearScale, Tooltip } from 'chart.js'
  import { onBeforeUnmount, onMounted, ref } from 'vue'

  Chart.register(RadarController, RadialLinearScale, PointElement, LineElement, Tooltip, Legend)

  const radarCanvas = ref(null)
  let radarChart = null

  const Utils = {
    color: index => ['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0'][index % 4],
    transparentize: (color, opacity = 0.5) => {
      const r = Number.parseInt(color.slice(1, 3), 16)
      const g = Number.parseInt(color.slice(3, 5), 16)
      const b = Number.parseInt(color.slice(5, 7), 16)
      return `rgba(${r},${g},${b},${opacity})`
    },
  }

  function getLineColor (ctx) {
    return Utils.color(ctx.datasetIndex)
  }

  function alternatePointStyles (ctx) {
    const index = ctx.dataIndex
    return index % 2 === 0 ? 'circle' : 'rect'
  }

  function makeHalfAsOpaque (ctx) {
    return Utils.transparentize(getLineColor(ctx))
  }

  function make20PercentOpaque (ctx) {
    return Utils.transparentize(getLineColor(ctx), 0.8)
  }

  function adjustRadiusBasedOnData (ctx) {
    const v = ctx.parsed.y
    return v < 10
      ? 5
      : v < 25
        ? 7
        : v < 50
          ? 9
          : v < 75
            ? 11
            : 15
  }

  const data = {
    labels: ['A', 'B', 'C', 'D', 'E'],
    datasets: [
      {
        label: 'Dataset 1',
        data: [20, 10, 30, 50, 40],

      },
      {
        label: 'Dataset 2',
        data: [15, 25, 35, 45, 55],

      },
    ],
  }

  onMounted(() => {
    radarChart = new Chart(radarCanvas.value, {
      type: 'radar',
      data,
      options: {
        plugins: {
          legend: false,
          tooltip: false,
        },
        elements: {
          line: {
            backgroundColor: make20PercentOpaque,
            borderColor: getLineColor,
            fill: true, // 加這行就會有填色
          },
          point: {
            backgroundColor: getLineColor,
            hoverBackgroundColor: makeHalfAsOpaque,
            radius: adjustRadiusBasedOnData,
            pointStyle: alternatePointStyles,
            hoverRadius: 15,
          },
        },
        scales: {
          r: {
            grid: {
              color: 'white',
            },
            angleLines: {
              color: 'white',
            },
            pointLabels: {
              color: 'white',

            },

            ticks: {
              display: false, // 隱藏數字
              stepSize: 15, // 依你的資料範圍調整，這樣只會有 2~3 條主網格
            },

            pointLabels: {
              color: 'white',
              font: { size: 24 }, // 放大外圈標籤
            },

          },
        },
      },
    })
  })

  onBeforeUnmount(() => {
    if (radarChart) {
      radarChart.destroy()
    }
  })
</script>

<style>
canvas {

  display: block;
  max-width: 400px;
  margin: 0 auto;
}
</style>
