<template >
  <div class="slideinformation">
    <el-row class="title_line">
      <div class="address">杭州湖滨</div>
      <div class="title_button"><i class="el-icon-arrow-left"></i></div>
    </el-row>
    <el-row class="realtime_number">
      <el-col :span="24"><div class="rtime_num">实时总人数</div><div class="datadate">{{date}} {{time}}</div></el-col>
      <el-col :span="24" class="rtime_data"><div class="data-num">{{rtime_num}}</div><div class="growth">同期增长<span>{{growth}}</span></div></el-col>
    </el-row>
    <el-row class="trend">
      <div id="chartLine" style="width:340px; height:267px;"></div>
    </el-row>
    
    <h1>vuex 测试</h1>
  </div>
</template>

<script>

import echarts from 'echarts'
export default {
  name: 'SideInformation',
  props: {
    
  },
  data(){
    return {
        time: '',
        date: '',
        rtime_num:'34,324',
        growth:"11.5%"
    }
        
  },
  computed: {
    
  },
  mounted() {
    //this.setSort()
    //setInterval(this.updateTime(), 1000)
    this.drawLineChart()
    
  },
  created () {
        
        this.intervalId = setInterval(() => {
            this.updateTime()
        }, 1000)
    },
  methods: {
    setSort() {
      const el = this.$refs.dragSelect.$el.querySelectorAll('.el-select__tags > span')[0]
      this.sortable = Sortable.create(el, {
        ghostClass: 'sortable-ghost', // Class name for the drop placeholder,
        setData: function(dataTransfer) {
          dataTransfer.setData('Text', '')
          // to avoid Firefox bug
          // Detail see : https://github.com/RubaXa/Sortable/issues/1012
        },
        onEnd: evt => {
          const targetRow = this.value.splice(evt.oldIndex, 1)[0]
          this.value.splice(evt.newIndex, 0, targetRow)
        }
      })
    },

  //实时时间
  updateTime() {
    var cd = new Date();
    this.time = this.zeroPadding(cd.getHours(), 2) + ':' + this.zeroPadding(cd.getMinutes(), 2) + ':' + this.zeroPadding(cd.getSeconds(), 2);
    this.date = this.zeroPadding(cd.getFullYear(), 2) + '.' + this.zeroPadding(cd.getMonth()+1, 2) + '.' + this.zeroPadding(cd.getDate(), 2);
    //console.log(this.time, this.date)
  },

  zeroPadding(num, digit) {
    var zero = '';
    for(var i = 0; i < digit; i++) {
        zero += '0';
    }
    return (zero + num).slice(-digit);
  },
  //销毁时间更新
  beforeDestroy () {
    clearInterval(this.intervalId)
  },
  //echart图
  drawLineChart() {
    console.log('123');
                this.chartLine = echarts.init(document.getElementById('chartLine'));
                this.chartLine.setOption({
                    option:{
                      backgroundColor:'#2E3037'
                    },
                    title: {
                        text: '总人数趋势',
                        textStyle:{
                          fontSize: 13,
                          fontWeight: 'bolder',
                          color: '#fff'
                        }
                    },
                    tooltip: {
                        trigger: 'axis'
                    },
                    legend: {
                        data: ['昨天', '今天'],
                        textStyle:{
                          color:'#fff'
                        }
                    },
                    grid: {
                        
                        left: '3%',
                        right: '4%',
                        bottom: '3%',
                        containLabel: true
                    },
                    xAxis: {
                        type: 'category',
                        boundaryGap: false,
                        data: ['12：00', '13:00', '14:00', '15:00', '周五', '周六', '周日'],
                        axisLine:{
                         // axisLine坐标轴轴线样式设置
                        lineStyle:{
                            color:'#fff', // 坐标轴轴线颜色设置
                            width:1, // 坐标轴线线宽。
                        }
                    },
                    },
                    yAxis: {
                        type: 'value',
                         axisLine: {
                          show: false
                        },
                    },
                    series: [
                        {
                            name: '昨天',
                            type: 'line',
                            stack: '总量',
                            data: [120, 132, 101, 134, 90, 230, 210]
                        },
                        {
                            name: '今天',
                            type: 'line',
                            stack: '总量',
                            data: [220, 182, 191, 234, 290, 330, 310]
                        }
                    ]
                });
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
.title_line{
  height: 33px;
  margin-bottom: 23px;
}
.address{
  margin-left: 13px;
  width: 287px;
  color: #fff;
  line-height: 33px;
  font-family: "Helvetic Neue";
  font-size: 24px;
  font-weight:bold;
  border-right: 1px rgba(255,255,255,0.1) solid;
  float: left;


}
.title_button{
  color:#fff;
  float: left;
  margin-left:15px;
  i{
    display: block;
    line-height: 33px;
    font-size: 20px;
    opacity: 0.6;
    cursor: pointer;
  }
}
.realtime_number{
  width: 340px;
  height: 99px;
  background: #2E3037;
  margin: 0 auto;
  box-sizing: border-box;
  padding: 16px 0 11px 16px;
  font-size: 13px;
  color:#fff;
  font-family: 'PingFangSC-Regular, sans-serif';
  .rtime_num{
    height: 18px;
    line-height: 18px;
    color: #fff;
    margin-right: 144px;
    float: left;
  }
  .datadate{
    float: left;
  }
  
}
.rtime_data{
  height: 42px;
  margin-top: 12px;
  font-family: 'PingFangSC-Regular, sans-serif';
  .data-num{
    line-height: 42px;
    font-size: 30px;
    margin-right: 16px;
    float: left;

  }
  .growth{
    float: left;
    font-size: 12px;
    line-height: 17px;
    color: rgba(255,255,255,0.6);
    margin-top:19px;
    
    
  }
  .growth span{
      color:#00d7bf

    }
}
.chartLine{
  width: 340px;
  height: 267px;
}

</style>
