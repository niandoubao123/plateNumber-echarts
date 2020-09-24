<template>
  <div id="app">
    <!-- <div id="chartLineBox" style="width: 90%;height: 70vh;"> </div> -->
    <key-bord></key-bord>
  </div>
</template>

<script>
 import echarts from 'echarts'
 import keyBord from './components/keyBord/index.vue'
export default {
  name: 'App',
  components: {
    keyBord
  },
  mounted(){
    this.chartLine = echarts.init(document.getElementById('chartLineBox'));
    // 指定图表的配置项和数据
    var option = {
      title: {
        text: '一级标题',
        subtext: '二级标题'
      },
      // tooltip: {              //设置tip提示
      //   trigger: 'axis',
      //   axisPointer: {        //鼠标悬浮到图上，可以出现标线和刻度文本。
      //     type: 'cross'
      //   },
      // },
      tooltip: {     //好看一些的提示
        trigger: 'axis',
        axisPointer: {
          type: 'cross'
        },
        backgroundColor: 'rgba(245, 245, 245, 0.8)',
        borderWidth: 1,
        borderColor: '#ccc',
        padding: 10,
        textStyle: {
          color: '#000'
        },
        // position: function (pos, params, el, elRect, size) {    //定位
        //   var obj = {top: 10};
        //   obj[['left', 'right'][+(pos[0] < size.viewSize[0] / 2)]] = 30;
        //   return obj;
        // },
        extraCssText: 'width: 170px'
      },
      axisPointer: {          //鼠标悬浮到图上，出现标线和刻度文本的颜色。
          link: {xAxisIndex: 'all'},
          label: {
            backgroundColor: '#777'
          }
      },
      legend: {               //设置区分（哪条线属于什么）   标识
        data:['平均成绩','学生成绩']
      },
      color: ['#8AE09F', '#FA6F53'],       //设置区分（每条线是什么颜色，和 legend 一一对应）
      xAxis: {                //设置x轴
        type: 'category',
        boundaryGap: true,     //坐标轴两边不留白
        data: ['2019-1-1', '2019-2-1', '2019-3-1', '2019-4-1', '2019-5-1', '2019-6-1', '2019-7-1','2019-8-1','2019-9-1','2019-10-1','2019-11-1','2019-12-1'],
        name: '日期',           //X轴 name
        nameTextStyle: {        //坐标轴名称的文字样式
            color: 'black',   //坐标轴名称颜色
            fontSize: 16,
            padding: [0, 0, 0, 20]
        },
        axisLine: {             //坐标轴轴线相关设置。
            lineStyle: {
              color: 'black',   //x轴颜色
            }
        }
      },
      yAxis: {
        type: 'value',
        name: '数量(个)',
        nameTextStyle: {
            color: 'black',
            fontSize: 16,
            padding: [0, 0, 10, 0]
        },
        axisLine: {
            lineStyle: {
              color: 'black',
            }
        }
      },
      series: [                       //画的线数组
        {
          name: '平均成绩',
          data:  [220, 232, 201, 234, 290, 230, 220,12,280,325,256,199],
          type: 'line',               // 类型为折线图
          lineStyle: {                // 线条样式 => 必须使用normal属性
              normal: {
                color: '#8AE09F',
              }
          },
          markPoint:{                 //最高最低点
            data: [
              {name: '年最高', value: 325, xAxis: 9, yAxis: 325},
              {name: '年最低', value: 12, xAxis: 7, yAxis: 12}
            ]
          },
          markLine: {      //均值线
            lineStyle: {
              normal: {
                type: 'solid',
                color:'orange'
              }
            },
            data: [
              {
                name: '平均值线',
                yAxis: 280 // 数值类型，对应y轴坐标
              }
            ]
            // data: [      //这是第二种
            //   {type: 'average', name: '平均值'}
            // ]
          },
          markArea: {       //阴影
            silent: true,
            itemStyle: {
              normal: {
                color: {
                  type: 'linear',      //渐变
                  x: 0,
                  y: 0,
                  x2: 0,
                  y2: 1,
                  colorStops: [{
                      offset: 0, color: 'rgba(0,0,0,0.1)' // 0% 处的颜色
                  }, {
                      offset: 1, color: '#fff' // 100% 处的颜色
                  }],
                  global: false // 缺省为 false
                },
                // borderWidth: 1,
                // borderType: 'dashed'
              }
            },
            data: [[{
              name: '均值线',
              yAxis: 280 // 阴影区域上边界
            }, {
              yAxis: 0 // 阴影区域下边界
            }]]
          }
        },
        {
          name: '学生成绩',
          data: [120, 200, 150, 80, 70, 110, 130,99,220,150,50,120],
          type: 'line',
          lineStyle: {
              normal: {
                color: '#FA6F53',
              }
          },
        }
      ]
    };
    // 使用刚指定的配置项和数据显示图表。
    this.chartLine.setOption(option);
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
