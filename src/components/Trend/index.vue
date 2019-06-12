<template >

  
    <div class="trend">
      <div :id="lists.id" style="width:100%; height:100%;"></div>
   
   </div> 
    
</template>

<script>

import echarts from 'echarts'

export default {
  name: 'Trend',
  props: {
    lists:{
      type:Object,
      requied:true
    }
  },
  data(){
    return {
        
    }
        
  },
  computed: {
    
  },
  mounted() {
    
    this.drawLineChart()
    
  },
  
  methods: {
  //echart图
  drawLineChart() {
  console.log(this.lists.arr,'123')
  var dataaar = this.lists.arr;
  
  var option = {
		title: {
      text: '总人数趋势',
      textStyle:{
      fontSize: 13,
      fontWeight: 'bolder',
      color: '#fff'
      }
    },
    align:'center',
    grid: {
                        
                        left: '-3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },

    backgroundColor:'#2E3037',
		tooltip: {
			trigger: 'axis'
		},
		xAxis: {
			type: 'category',
			splitLine: {
				show: false
      },
      boundaryGap:false,
      
      //splitNumber : 7,
      
      axisLine:{
        lineStyle:{
         color:'#fff', // 坐标轴轴线颜色设置
         width:1, // 坐标轴线线宽。
          }
        },
        axisLabel:{
          align:'cente'
        },
        axisTick:{
        alignWidthLabel:true
        },
        

        //data: ['12：00','13:00', '14:00', '15:00']
        
        data: ['12：00','','13:00','', '14:00','', '15:00']

		},
		yAxis: {
      type: 'value',
			boundaryGap: [0, '100%'],
			splitLine: {
				show: true
      },
      scale : true,
      max : 600,
      min : 0,
      splitNumber : 5,
      //boundaryGap : [ 0.2, 0.2 ],
      axisLine: {show:false},
      axisTick: {show:false},
      axisLabel: {show:false}
    },
    
		series: [{
                            name: '昨天',
                            type: 'line',
                            smooth:true,
                            stack: '总量',
                            data: [120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name: '今天',
                            smooth:true,
                            type: 'line',
                            stack: '总量',
                            data: [220, 182, 191, 234, 290, 330, 310]
                        }

				
]
  };
  var chartLine = echarts.init(document.getElementById(this.lists.id));

  chartLine.setOption(option);
               
            }




  },
  
  
}
</script>

<style scoped lang="scss">
@import '~scss_vars';
.slideinformation{
  width: 372px;
  background: #202126;
  padding:23px 16px 35px;
  box-sizing: border-box;
}
.trend{
  width: 340px;
  height: 267px;
}
.chartLine{
  width: 340px;
  height: 267px;
}

</style>
