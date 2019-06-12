<template >
  <div class="camera " v-show='isShow'>
    <el-row class="content">
      <img src="https://gw.alicdn.com/tfs/TB1U8SHcCWD3KVjSZSgXXcCxVXa-326-181.png" alt="" class="camera_Pic">
      <div class=" butn fullscreen-btn">
        <img src="https://gw.alicdn.com/tfs/TB1wBCLcBKw3KVjSZFOXXarDVXa-28-28.png" alt="">
      </div>
      <div class=" butn close-btn" @click="cloth()">
        <img src="https://gw.alicdn.com/tfs/TB1Jn9FcBiE3KVjSZFMXXbQhVXa-24-24.png" alt="">
      </div>
    </el-row>
    <el-row class="camera_message">
      <div class="road_name">点位名称</div>
      <div class="current_number">当前人数 <p class="num">23</p></div>
      <div class="camera_click">
        <img src="https://gw.alicdn.com/tfs/TB1udWQcBiE3KVjSZFMXXbQhVXa-75-75.png" alt="">
      </div>
      <el-row class="tool_line">
      <div class="butn circle_butn linechart" :class="{active: lineactive == true}" @click="linechart()">
        <img src="https://gw.alicdn.com/tfs/TB190SIcEGF3KVjSZFoXXbmpFXa-16-14.png" alt="">
      </div>
      <div class="butn circle_butn collect" :class="{active : collectactive == true}" @click="collect()">
        <img src="https://gw.alicdn.com/tfs/TB1XdWRcq1s3KVjSZFAXXX_ZXXa-16-16.png" alt="">
      </div>
      <div class="arrow">
        <i class="arrow_btn arrow-left el-icon-arrow-left"></i>
        <i class="arrow_btn arrow-right el-icon-arrow-right"></i>
      </div>
      
    </el-row>
    <el-row class="camera_line">
      <Trend :lists="lists"></Trend>
    </el-row>
    </el-row>
    
    
   
  </div>
</template>

<script>

import Trend from '../Trend/index';
import echarts from 'echarts';
export default {
  name: 'Camera',
  props: {
    
  },
  components: {
   Trend
  },
  
  data() {
      return {
        tableData: [{
          point: '点1',
          num: '12'
        }, {
          point: '点2',
          num: '2'
        }, {
          point: '点3',
          num: '3'
        }, {
          point: '点4',
          num: '5'
        },
        {
          point: '点5',
          num: '7'
        },
        {
          point: '点6',
          num: '9'
        }],
        isShow:true,
        lineactive:false, //折线图按钮是否选中
        collectactive:false,    //收藏按钮是否选中
        lists:{
          id:'localLine',
          arr:[120, 1, 2, 3, 4, 230, 210]
        }
      }
    },
    mounted() {
    
    
    
  },
  
  
  methods: {
      linechart() {
        this.lineactive = this.lineactive == false ? true: false
        //this.lineactive = true;
      },
      collect() {
        
        this.collectactive = this.collectactive == false ? true: false
      },
      cloth() {
        this.isShow = !this.isShow;
      }
      
}
}
</script>

<style scoped lang="scss">
@import '~scss_vars';
.camera{
  width: 326px;
  background: #374148;
  position: fixed;
  top: 17px;
  right:44px;
  border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    
  .content{
  width: 326px;
  height: 181px;
  position: relative;
  font-family: 'PingFangSC-Regular, sans-serif';
  }
  .camera_Pic{
    width: 100%;
    height:100%;
  }
  .butn{
    position: absolute;
    cursor: pointer;
    
    
  }
  .butn img{
      width: 100%;
      height: 100%;
    }
  .fullscreen-btn{
    width: 26px;
    height: 26px;
    top:10px;
    left: 10px;
  }
  .close-btn{
    width: 16px;
    height: 16px;
    right: 16px;
    top:15px;
  }
  .camera_message{
    padding: 14px 18px 10px 13px;
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    

    .road_name{
      height: 22px;
      line-height: 22px;
      color: #fff;
      font-size: 16px;
    }
    .current_number{
      height:20px;
      line-height: 20px;
      color: rgba(255,255,255,0.45);
      font-size: 14px;
      margin-top: 15px;
    }
    p{
      margin:0;
      padding:0;
    }
    .num{
      color: #fff;
      display: inline-block;
      padding-left: 14px;
      
    }
    .camera_click{
      cursor: pointer;
      width: 75px;
      height:75px;
      position: absolute;
      top: 10px;
      right:8px;

    }
    

  }
  .tool_line{
      height: 28px;
      margin-top: 29px;
      
    }
    .circle_butn{
      position: relative;
      float: left;
      width: 26px;
      height: 26px;
      border-radius: 50%;
      background: rgba(255,255,255,0.17);
      display:flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      margin-right: 12px;
      
    }
    .active{
      background: #4880FF;
      }
    .linechart img{
      width: 15.4px;
      height: 14.12px;
      
    }
    .collect img{
      width: 15.81px;
      height:15.02px;

    }
    .arrow{
      width: 55px;
      height: 16px;;
      float: right;
      margin-top: 5px;
      
    }
    .arrow_btn{
      color: #fff;
      font-size: 16px;
      float: left;
      cursor: pointer;
      
    }
    .arrow-right{
      
      float: right;
    }
    .camera_line{
      position: absolute;
      width: 326px;
      height:170px;
      .trend{
        width: 326px;
        height:152px;
        padding-bottom: 18px;
      }
    }
    
    


}





</style>
