<template>
  <div class="outbox">
    <div id="echart1" ref="echart1"></div>
  </div>
</template>
<script>
export default {
  name: "echart1",
  data() {
    return {
      ylinedata: [],
      xdata: [],
      barbaldata: [],
      run: null
    };
  },
  mounted() {
    var that = this;
    var aa = 30 + Math.random().toFixed(4) * 4;
    for (var i = 0; i < 100; i++) {
      that.barbaldata.push(0);
      that.ylinedata.push(aa);
      that.xdata.push(i);
    }
    that.barbaldata.splice(
      that.barbaldata.length - 1,
      1,
      that.ylinedata[that.ylinedata.length - 1]
    );
    that.drawLine();
    that.run = function() {
      console.log(new Date().getSeconds());
      var b = 30 + Math.random().toFixed(4) * 4;
      if (
        Number(new Date().getSeconds()) == 58 ||
        Number(new Date().getSeconds()) == 16 ||
        Number(new Date().getSeconds()) == 29 ||
        Number(new Date().getSeconds()) == 31 ||
        Number(new Date().getSeconds()) == 43
      ) {
        var b = 38 + Math.random().toFixed(4) * 20;
      }
      that.xdata.shift();
      that.ylinedata.shift();
      that.xdata.push(b);
      that.ylinedata.push(b);
      that.barbaldata.splice(that.barbaldata.length - 1, 1, b);
      var fps = 10;
      setTimeout(function() {
        window.requestAnimationFrame(that.run);
        that.drawLine();
      }, 1800 / fps);
    };
    that.run();
  },
  methods: {
    drawLine() {
      var that = this;
      var myChart = this.$echarts.init(this.$refs.echart1);
      myChart.setOption({
          backgroundColor: "rgba(0,5,21,0.8)",
        /*        backgroundColor: "#1a3b44", */
        grid: {
          height: "150",
          top: "30",
          bottom: "10",
          right: "20",
          left: "20"
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: that.xdata,
          axisTick: {
            show: false
          },
          axisLabel: {
            show: false
          },
          axisLine: {
            lineStyle: {
              color: "#3a3e4d",
              width: 1
            }
          }
        },
        yAxis: {
          type: "value",
          show: false
        },
        series: [
          {
            data: that.ylinedata,
            type: "line",
            animation: false,
            smooth: true,
            symbol: "none",
             markLine: {
                silent: true,
                symbol: "none",
                  label: {
                formatter: function(val) {
                  return (val.value = "");
                }
              },
                data: [{
                    yAxis: 5,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                }, {
                    yAxis: 13,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                }, {
                    yAxis: 21,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                }, {
                    yAxis: 29,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                }, {
                    yAxis: 37,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                },
                 {
                    yAxis: 45,
                     lineStyle: {
                    normal: {
                      color: "#323f46"
                    }
                  }
                 }
                ]
            },
            lineStyle: {
              color: {
                type: "linear",
                colorStops: [
                  {
                    offset: 0,
                    color: "#009cff", // 0% 处的颜色,
                    transition: 2
                  },
                  {
                    offset: 0.66,
                    color: "#009cff", // 66% 处的颜色
                    transition: 2
                  },
                  {
                    offset: 1,
                    color: "#fff", // 100% 处的颜色
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
                  type: "linear",
                  x: 0,
                  y: 0,
                  x2: 0,
                  y2: 1,
                  colorStops: [
                    {
                      offset: 0,
                      color: "rgba(255,255,255,0.3)" // 0% 处的颜色
                    },
                  /*   {
                      offset: 0.66,
                      color: "rgba(255,255,255,0.3)" 
                    }, */
                    {
                      offset: 1,
                      color: "rgba(255,255,255,0)" // 100% 处的颜色
                    }
                  ],
                  globalCoord: false // 缺省为 false
                }
              }
            }
          },

          {
            barWidth: 2,
            type: "bar",
            data: that.barbaldata,
            animation: false,
            itemStyle: {
              normal: {
                color: "#fff"
              }
            },
            markPoint: {
              animation: false,
              symbol: "circle",
              data: [{ type: "max" }],
              symbolSize: 10,
              itemStyle: {
                normal: {
                  color: "#020b1c",
                  borderColor: "#fff",
                  borderWidth: "2",
                  label: {
                    show: false
                  }
                }
              }
            }
          }
        ]
      });
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
};
</script>
<style scoped>
.outbox {
  width: 700px;
  height: 180px;
  z-index: 99;
/*   background-color: #1a3b44; */
  position: relative;
}

#echart1 {
  width: 700px;
  height: 180px;

}
</style>
