<template>
  <div id="app">
    <div class="right-menu">
      <img :src="imgMeasureSrc" @click="imgMeasure">
    </div>
    <baidu-map class="map"  center="北京" @ready="handler">

    </baidu-map>
  </div>
</template>

<script>
  import Vue from 'vue'
  import BaiduMap from 'vue-baidu-map'
  import createMeasureAreaTool from 'bmaplib.distancetool'
  Vue.use(BaiduMap, {
    // ak 是在百度地图开发者平台申请的密钥 详见 http://lbsyun.baidu.com/apiconsole/key */
    ak: 'ak'
  })
export default {
  name: 'App',
  data () {
    return {
      //菜单栏点击事件图片切换
      imgMeasureURL:[require('@/assets/menu/measure-common.png'),require('@/assets/menu/measure-checked.png')],
      imgMeasureIndex:0,
    }
  },
  computed:{
    //菜单栏图标切换，计算图片数组[index]
    imgMeasureSrc(){
      return this.imgMeasureURL[this.imgMeasureIndex]
    }
  },
  methods: {
    handler({ BMap, map }) {
      this.distanceTool = createMeasureAreaTool(map);//初始化测距工具
    },
    imgMeasure(e){
      this.imgMeasureIndex=(this.imgMeasureIndex+1)%(this.imgMeasureURL).length;
      if(this.imgMeasureIndex==1){
        const {distanceTool} = this;
        distanceTool && distanceTool.open();
      }
    },
  }
}

</script>

<style>
  #app{
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: auto;
    overflow-x: hidden;
    background: #fff;
  }
  .map{
   width: 100%;
    height: 100%;
  }
  .right-menu{
    width: 30px;
    height: 23px;
    background: #FFFFFF;
    text-align: center;
    position: absolute;
    right: 27px;
    top: 15px;
    z-index: 9;
  }
  .right-menu img{
    cursor:pointer;
  }
</style>
