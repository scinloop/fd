<template>
  <div>
    <div id="bottomLeftChart1" style="width:11.25rem;height:6.0rem;"></div>
  </div>
</template>

<script>
import echartMixins from "@/utils/resizeMixins";
import get from "@/utils/bottomleft"
export default {
  data() {
    return {
      chart: null,
      Listdata:null
    };
  },
  mixins: [echartMixins],
  mounted() {
    this.draw();
    // this.fetchdata();
  },
  methods: {
    fetchdata() {
      console.log("fetchdata")
      get('/api').then(response => {
        this.Listdata = response.data
        console.log(response.data)
      }).catch(error => {
        console.log(error)
      })

    },
    draw() {
      // 基于准备好的dom，初始化echarts实例
      this.chart = this.$echarts.init(document.getElementById("bottomLeftChart1"));
      //  ----------------------------------------------------------------
      let category = [
        "市区",
        "万州",
        "江北",
        "南岸",
        "北碚",
        "綦南",
        "长寿",
        "永川",
        "璧山",
        "江津",
        "城口",
        "大足",
        "垫江",
        "丰都",
        "奉节",
        "合川",
        "江津区",
        "开州",
        "南川",
        "彭水",
        "黔江",
        "石柱",
        "铜梁",
        "潼南",
        "巫山",
        "巫溪",
        "武隆",
        "秀山",
        "酉阳",
        "云阳",
        "忠县",
        "川东",
        "检修"
      ];
      let lineData = [
        18092,
        20728,
        24045,
        28348,
        32808,
        36097,
        39867,
        44715,
        48444,
        50415,
        56061,
        62677,
        59521,
        67560,
        18092,
        20728,
        24045,
        28348,
        32808,
        36097,
        39867,
        44715,
        48444,
        50415,
        36097,
        39867,
        44715,
        48444,
        50415,
        50061,
        32677,
        49521,
        32808
      ];
      let barData = [
        4600,
        5000,
        5500,
        6500,
        7500,
        8500,
        9900,
        12500,
        14000,
        21500,
        23200,
        24450,
        25250,
        33300,
        4600,
        5000,
        5500,
        6500,
        7500,
        8500,
        9900,
        22500,
        14000,
        21500,
        8500,
        9900,
        12500,
        14000,
        21500,
        23200,
        24450,
        25250,
        7500
      ];
      let rateData = [];
      for (let i = 0; i < 33; i++) {
        let rate = barData[i] / lineData[i];
        rateData[i] = rate.toFixed(2);
      }

      let option = {
        title: {
          text: "",
          x: "center",
          y: 0,
          textStyle: {
            color: "#B4B4B4",
            fontSize: 16,
            fontWeight: "normal"
          }
        },
        // 悬浮显示数据tooltip
        tooltip: {
          trigger: "axis",
          backgroundColor: "rgba(255,255,255,0.1)",
          axisPointer: {
            type: "shadow",
            label: {
              show: true,
              backgroundColor: "#7B7DDC"
            }
          }
        },

        //折线标注
        legend: {
          data: ["风速", "功率", "贯通率"],
          textStyle: {
            color: "#B4B4B4"
          },
          top: "0%"
        },
        // grid: {
        //   x: "8%",
        //   width: "88%",
        //   y: "4%"
        // },
        xAxis: {
          data: category,
          axisLine: {
            lineStyle: {
              color: "#B4B4B4"
            }
          },
          axisTick: {
            show: false
          }
        },
        yAxis: [
          {
            name:"风速",
            splitLine: { show: false },
            axisLine: {
              lineStyle: {
                color: "#B4B4B4"
              }
            },

            axisLabel: {
              formatter: "{value} "
            }
          },
          {
            splitLine: { show: false },
            axisLine: {
              lineStyle: {
                color: "#B4B4B4"
              }
            },
            axisLabel: {
              formatter: "{value} "
            }
          }
        ],
        series: [
          {
            name: "功率",
            type: "line",
            smooth: true,
            showAllSymbol: true,
            symbol: "emptyCircle",
            symbolSize: 8,
            yAxisIndex: 1,
            itemStyle: {
              normal: {
                color: "#F02FC2"
              }
            },
            data: rateData
          },

          {
            name: "风速",
            type: "line",
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: "#956FD4" },
                  { offset: 1, color: "#3EACE5" }
                ])
              }
            },
            data: barData
          },
          {
            name: "贯通率",
            type: "line",
            barWidth: 10,
            itemStyle: {
              normal: {
                barBorderRadius: 5,
                color: new this.$echarts.graphic.LinearGradient(0, 0, 0, 1, [
                  { offset: 0, color: "rgba(122,20,165,0.8)" },
                  { offset: 1, color: "#2a1abb" }
                ])
              }
            },
            data: lineData
          }
        ]
      };
      this.chart.setOption(option);
    }
  },
  destroyed() {
    window.onresize = null;
  }
};
</script>

<style lang="scss" scoped>
</style>
