<template>
  <div id="guageChart" style="width:100%;height: 100%"></div>
</template>
<script>
  import echarts from 'echarts'

  export default {
    name: 'guageChart',
    props: {
      chartOptions: Object,
      chartData: Object

    },
    methods: {
      init () {
        const chart = echarts.init(document.getElementById('guageChart'))
        window.addEventListener('resize', function () {
          chart.resize()
        })
        const option = {
          tooltip: {
            formatter: '{a} <br/>{b} : {c}%'
          },
          series: [
            {
              name: 'inhale',
              type: 'gauge',
              min: 0,
              max: 1000,
              detail: {
                formatter: '{value}ml',
                fontSize: 18,
                offsetCenter: [0, '50px']
              },
              data: [{value: 50, name: 'Inhale flow'}],
              center: ['25%', '50%'],
              radius: '80%',
              title: {
                offsetCenter: [0, '80px']
              },
              axisLine: {
                lineStyle: {
                  // color: [],
                  width: 20
                }
              },
              splitLine: {
                length: 20
              }
            },
            {
              name: 'exhale',
              type: 'gauge',
              min: 0,
              max: 1000,
              detail: {
                formatter: '{value}ml',
                fontSize: 18,
                offsetCenter: [0, '50px']
              },
              data: [{value: 50, name: 'Exhale flow'}],
              center: ['75%', '50%'],
              radius: '80%',
              title: {
                offsetCenter: [0, '80px']
              },
              axisLine: {
                lineStyle: {
                  // color: [],
                  width: 20
                }
              },
              splitLine: {
                length: 20
              }
            }
          ]
        };

        setInterval(function () {
          option.series[0].data[0].value = (Math.random() * 1000).toFixed(2) - 0;
          option.series[1].data[0].value = (Math.random() * 1000).toFixed(2) - 0;
          chart.setOption(option);
        }, 2000);
      }

    },
    mounted () {
      this.init()
    }
  }
</script>
