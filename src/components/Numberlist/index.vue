<template >
  <div class="numberlist">
    <el-row class="title_line">
      <p class="title">各点位人数</p>
     </el-row>
    <el-row class="click_button">
      <div class="point_name">点位名称</div><div class="current_number" @click="setOrderType()">当前人数<div class="icon_style"><i class='caret-top' :class="{ active:orderType==1 }"></i><i class="caret-bottom" :class="{ activebottom:orderType==2 }"></i></div></div>
    </el-row>
    <div class="list_box" id ="list_box">
      <ul class="list" id = "num_list">
        <li v-for="(p,index) in filterPersons" :key="index" class="list_item">
                  <div class="address_point">{{p.point}}</div>
                  <div class="people_num">{{p.num}}</div>
                    
                </li>          
      </ul>
       
    </div>
   
  </div>
</template>

<script>


export default {
  name: 'Numberlist',
  props: {
    
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
        orderType: 0    //0代表原本，1代表升序，2代表降序
      }
    },
    mounted() {
    
    this.getheight()
    
  },
  computed:{
    filterPersons(){
        //取出相关数据
        const {tableData,orderType}=this 
        const a2 = [...tableData];
        console.log(a2,'a2')
        //最终需要显示的数组
        let fPersons = tableData;
        //对persons进行过滤
        //fPersons=tableData.filter(p=> p.num.indexOf(tableData)!==-1)
        console.log(tableData);
        //排序
        if(orderType!==0){
          //console.log('222')
            fPersons.sort(function(p1,p2){    //返回负数P1在前，返回正数P2在前
                //1代表升序，2代表降序
                if(orderType===2){
                    return p2.num-p1.num
                }else{
                    return p1.num-p2.num
                }
                //return p2.num-p1.num
            })
        }

        
        return fPersons
    }
},
  
  methods: {
      
      getheight() {
        console.log('1111');
        console.log(document.getElementById("list_box").offsetHeight);
        var listH = document.getElementById("list_box").offsetHeight;
        document.getElementById("num_list").style.height = listH + 'px';
      },
      setOrderType(){
        if(this.orderType == 0) {
          this.orderType = 1 //转成升序
        } else if (this.orderType == 1) {
          this.orderType = 2
        } else if (this.orderType == 2){
          this.orderType = 1
        }

      }
    }
}
</script>

<style scoped lang="scss">
@import '~scss_vars';
ul,li{ padding:0;margin:0;list-style:none}
.numberlist{
  //display:flex;
  width: 340px;
  height: 100%;
  background: #2E3037;
  box-sizing: border-box;
  margin-top: 16px;
  flex: 1;
  display: flex;
  flex-direction: column;
  min-height: 0;
  overflow: scroll;
  

.title_line{
  height: 47px;border-bottom: 1px rgba(255,255,255,0.1) solid;
  .title{
    font-size: 13px;
    line-height: 18px;
    font-family: "Helvetic Neue";
    color: #fff;
    padding-left: 17px;

  }
}
.click_button{
  margin:0 auto;
  width: 310px;
  height:18px;
  font-size: 13px;
  color: #fff;
  opacity: 0.3;
  line-height: 18px;
  font-family: "Helvetic Neue";
  margin-top: 11.5px;
  margin-bottom: 11px;
  .point_name{
    float: left;
  }
  .current_number{
    float:right;
    cursor: pointer;
    width:71px;
  }

}
.icon_style{
  width: 8px;
  float:right;
  i{
    font-size: 8px;
  }
  .caret-top{
    display: inline-block;
    position:absolute;
    top: 4px;
    width: 0;
    height: 0;
    border: 0;
    content: "";
    border-top: none;
    border-bottom: 5px solid #fff;
    border-right: 5px solid transparent;
    border-left: 5px solid transparent;
  }
  .caret-bottom{
    display: inline-block;
    width: 0;
    position:absolute;
    bottom: 2px;
    height: 0;
    border: 0;
    content: "";
    border-bottom: none;
    border-top: 5px solid #fff;
    border-right: 5px solid transparent;
    border-left: 5px solid transparent;
  }
  .active{
    border-bottom-color: #626eff 
  }
  .activebottom{
    border-top-color: #626eff 
  }
}

.list_box{
  width:340px;
  flex:1;
  
}
.list{
  //overflow-y: scroll;
  list-style: none;
  width: 340px;
  //background: #fff;
  height: 100px;
  overflow: scroll;
  
  
}
.list_item{
width: 310px;
padding: 0 15px;
height: 40px;
line-height: 40px;
font-size: 13px;
color: #fff;
font-family: 'PingFangSC-Regular, sans-serif';
display: flex;
}
.list_item:hover{

color: #fff;
background-color: #33363d;color: #626eff;font-family: 'PingFang-SC-Bold'
}
.address_point{
  width: 240px;
}
.people_num{
  width:70px;
  text-align: right;
}
.el-table__header{
  width: 100%;
}




}

</style>
