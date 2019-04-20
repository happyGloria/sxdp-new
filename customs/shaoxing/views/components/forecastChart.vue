<template>
  <div class="forecast-chart">
    <table class="summarization" cellspacing="0" cellpadding="0" border="0">
      <tr v-for="item in forecastData.summarization" :key="item.name">
        <td width="20%"><div class="dot">...</div></td>
        <td width="30%">{{item.value}}</td>
        <td class="text-gray">{{item.name}}({{item.unit}})</td>
      </tr>
    </table>
    <div ref="chart" class="chart"></div>
  </div>
</template>
<script>
const EChart = require('echarts')
export default {
    props: {
        forecastData: Object
    },
    data() {
        return {
            ylinedata: [],
            xdata: [],
            barbaldata: [],
            run: null
        }
    },
    mounted() {
        var that = this
        var aa = 30 + Math.random().toFixed(4) * 4
        for (var i = 0; i < 100; i++) {
            that.barbaldata.push(0)
            that.ylinedata.push(aa)
            that.xdata.push(i)
        }
        that.barbaldata.splice(
            that.barbaldata.length - 1,
            1,
            that.ylinedata[that.ylinedata.length - 1]
        )
        that.drawLine()
        that.run = function() {
            console.log(new Date().getSeconds())
            var b = 30 + Math.random().toFixed(4) * 4
            if (
                Number(new Date().getSeconds()) == 58 ||
                Number(new Date().getSeconds()) == 16 ||
                Number(new Date().getSeconds()) == 29 ||
                Number(new Date().getSeconds()) == 31 ||
                Number(new Date().getSeconds()) == 43
            ) {
                var b = 38 + Math.random().toFixed(4) * 20
            }
            that.xdata.shift()
            that.ylinedata.shift()
            that.xdata.push(b)
            that.ylinedata.push(b)
            that.barbaldata.splice(that.barbaldata.length - 1, 1, b)
            var fps = 10
            setTimeout(function() {
                window.requestAnimationFrame(that.run)
                that.drawLine()
            }, 1800 / fps)
        }
        that.run()
    },
    methods: {
        drawLine() {
            let myChart = EChart.init(this.$refs.chart)
            let option = {
                /* backgroundColor: 'rgba(0,5,21,0.8)', */
                /*        backgroundColor: "#1a3b44", */
                grid: {
                    height: '150',
                    top: '10',
                    bottom: '10',
                    right: '20',
                    left: '20'
                },
                xAxis: {
                    type: 'category',
                    boundaryGap: false,
                    data: this.xdata,
                    axisTick: {
                        show: false
                    },
                    axisLabel: {
                        show: false
                    },
                    axisLine: {
                        lineStyle: {
                            color: '#3a3e4d',
                            width: 1
                        }
                    }
                },
                yAxis: {
                    type: 'value',
                    show: false
                },
                series: [
                    {
                        data: this.ylinedata,
                        type: 'line',
                        animation: false,
                        smooth: true,
                        symbol: 'none',
                        markLine: {
                            silent: true,
                            symbol: 'none',
                            label: {
                                formatter: function(val) {
                                    return (val.value = '')
                                }
                            },
                            data: [
                                {
                                    yAxis: 5,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                },
                                {
                                    yAxis: 13,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                },
                                {
                                    yAxis: 21,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                },
                                {
                                    yAxis: 29,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                },
                                {
                                    yAxis: 37,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                },
                                {
                                    yAxis: 45,
                                    lineStyle: {
                                        normal: {
                                            color: '#323f46'
                                        }
                                    }
                                }
                            ]
                        },
                        lineStyle: {
                            color: {
                                type: 'linear',
                                colorStops: [
                                    {
                                        offset: 0,
                                        color: '#fff', // 0% 处的颜色,
                                        transition: 2
                                    },
                                     {
                                        offset: 0.98,
                                        color: '#009cff', // 66% 处的颜色
                                        transition: 2
                                    },
                                    {
                                        offset: 0.66,
                                        color: '#009cff', // 66% 处的颜色
                                        transition: 2
                                    },
                                    {
                                        offset: 1,
                                        color: '#fff', // 100% 处的颜色
                                        transition: 2
                                    }
                                ],
                                opacity: 0.4,
                                globalCoord: false // 缺省为 false
                            }
                        },
                        areaStyle: {
                            normal: {
                                color: {
                                    type: 'linear',
                                    x: 0,
                                    y: 0,
                                    x2: 0,
                                    y2: 1,
                                    colorStops: [
                                        {
                                            offset: 0,
                                            color: 'rgba(255,255,255,0.3)' // 0% 处的颜色
                                        },
                                        /*   {
                      offset: 0.66,
                      color: "rgba(255,255,255,0.3)" 
                    }, */
                                        {
                                            offset: 1,
                                            color: 'rgba(255,255,255,0)' // 100% 处的颜色
                                        }
                                    ],
                                    globalCoord: false // 缺省为 false
                                }
                            }
                        }
                    },

                    {
                        barWidth: 2,
                        type: 'bar',
                        data: this.barbaldata,
                        animation: false,
                        itemStyle: {
                            normal: {
                                color: '#fff'
                            }
                        },
                        markPoint: {
                            animation: false,
                            symbol: 'circle',
                            data: [{ type: 'max' }],
                            symbolSize: 10,
                            itemStyle: {
                                normal: {
                                    color: '#020b1c',
                                    borderColor: '#fff',
                                    borderWidth: '2',
                                    label: {
                                        show: false
                                    }
                                }
                            }
                        }
                    }
                ]
            }
            myChart.setOption(option)
        }
    },
    watch: {
        forecastData: {
            deep: true,
            handler(val) {
                /*  this.renderChart() */
            }
        }
    },
     destroyed() {
    window.cancelAnimationFrame(this.run());
    this.run = null;
    console.log(
      "%cwindow.cancelAnimationFrame(this.run())%c %c44",
      "color:red;font-size:36px;font-weight:bold",
      "",
      window.cancelAnimationFrame(this.run())
    );
  }
}
</script>
<style lang="less" scoped>
.forecast-chart {
    .chart {
        height: 150px;
    }
    .text-gray {
        color: #747474;
    }
    .summarization {
        width: 100%;
        font-size: 12px;
        margin-left: 10px;
        tr {
            line-height: 22px;
              &:first-of-type{
          /*   background: linear-gradient(to right, #080808 , #202126); */
          background-color: rgba(37,45,62,0.4)
            }
            &:first-of-type {
                /*  background: linear-gradient(to right, #080808 , #202126); */
            }
            // .dot{
            //     display: inline-block;
            //     vertical-align: super;
            // }
        }
    }
}
</style>
