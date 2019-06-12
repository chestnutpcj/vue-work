<template >
  <div class="slideinformation">
    <!-- <div class='allheight'> -->
      <el-row class="title_line">
      <div class="address">杭州湖滨</div>
      <div class="title_button"><i class="el-icon-arrow-left"></i></div>
    </el-row>
    <el-row class="realtime_number">
      <el-col :span="24"><div class="rtime_num">实时总人数</div><div class="datadate">{{date}} {{time}}</div></el-col>
      <el-col :span="24" class="rtime_data"><div class="data-num">{{rtime_num}}</div><div class="growth">同期增长<span>{{growth}}</span></div></el-col>
    </el-row>
    <Trend :lists="lists"></Trend>
    
    <Numberlist></Numberlist>
    
  </div>
</template>

<script>

import echarts from 'echarts'
import Trend from '../Trend/index'
import Numberlist from '../Numberlist/index'
export default {
  name: 'SideInformation',
  props: {
    
  },
  components: {
          Trend,
          Numberlist
    	},
  data(){
    return {
        time: '',
        date: '',
        rtime_num:'34,324',
        growth:"11.5%",
        lists:{
          id:'chartLine',
          arr:[120, 132, 101, 134, 90, 230, 210]
        }

    }
        
  },
  computed: {
    
  },
  mounted() {
    //this.setSort()
    //setInterval(this.updateTime(), 1000)
    
    
  },
  created () {
        
        this.intervalId = setInterval(() => {
            this.updateTime()
        }, 1000)
    },
  methods: {
    
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
  }
  
  
}
}
</script>

<style scoped lang="scss">
@import '~scss_vars';
.slideinformation{
  width: 372px;
  background: #202126;
  padding:23px 16px 35px;
  box-sizing: border-box;
  height: 100%;
  display: flex;
  flex-direction: column;
  

.allheight{
  height: 100%;
  //overflow: hidden;
  display: flex;
  flex-direction:column;
}
.test{
  flex: 1;
  //background: #fff;
  //margin-top: 10px;
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
  margin-bottom: 16px;
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
}
</style>
