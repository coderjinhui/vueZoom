<template>
  <div class="zoom-wrap" :style="{width:sSize.width+'px',height:sSize.height+'px'}">
    <div ref="small" @mouseover="mouseOver" @mousemove="move" @mouseout="mouseOut" class="small" :style="{width:sSize.width+'px',height:sSize.height+'px'}">
      <img :src="sImg">
      <div v-if="show" ref="mask" class="mask" :style="{width:mSize.width+'px',height:mSize.height+'px',top:mTop+'px',left:mLeft+'px'}"></div>
    </div>
    <div v-if="show" class="big" :style="{width:bSize.width+'px',height:bSize.height+'px'}">
      <img :src="bImg" :style="{width:bigW+'px',height:bigH+'px',top:imgTop+'px',left:imgLeft+'px'}">
    </div>
  </div>
</template>

<script>
  //放大镜
  /*
  * 需要参数
  * sImg 小图src 'http://xxxxx'
  * bImg 大图src 'http://xxxxx'
  * sSize 小图显示大小 {width:100,height:100}
  * bSize 大图显示大小 {width:100,height:100}
  * mSize 浮动块大小 {width:100,height:100}
  * */


    export default {
      props:{
        sImg:{type:String},
        bImg:{type:String},
        sSize:{type:Object},
        bSize:{type:Object},
        mSize:{type:Object}
      },
      data(){
        return{
          mX:0,
          mY:0,
          show:false
        }
      },
      computed:{
        bigW(){
          let mw=this.mSize.width;
          let sw=this.sSize.width;
          let bw=this.bSize.width;
          let ww=bw/mw*sw;
          return ww;
        },
        bigH(){
          let mh=this.mSize.height;
          let sh=this.sSize.height;
          let bh=this.bSize.height;
          let hh=bh/mh*sh;
          return hh;
        },
        mTop(){
          let top=this.mY-this.mSize.width/2;
          if(top<=0){
            top=0;
          }
          if(top>=(this.sSize.height-this.mSize.height)){
            top=this.sSize.height-this.mSize.height;
          }
          return top;
        },
        mLeft(){
          let left=this.mX-this.mSize.width/2;
          if(left<=0){
            left=0;
          }
          if(left>=(this.sSize.width-this.mSize.width)){
            left=this.sSize.width-this.mSize.width;
          }
          return left;
        },
        imgTop(){
          let bTop=this.mTop/this.sSize.height*this.bigH;
          return -bTop;
        },
        imgLeft(){
          let bLeft=this.mLeft/this.sSize.width*this.bigW;
          return -bLeft;
        }
      },
      created(){

      },
      methods:{
        mouseOver(e){
          this.mX=e.clientX-this.$refs.small.getBoundingClientRect().left;
          this.mY=e.clientY-this.$refs.small.getBoundingClientRect().top;
          this.show=true;
        },
        move(e){
          this.mX=e.clientX-this.$refs.small.getBoundingClientRect().left;
          this.mY=e.clientY-this.$refs.small.getBoundingClientRect().top;
        },
        mouseOut(){
          this.show=false;
        }
      }
    }
</script>

<style lang="less" type="text/less" scoped>
.zoom-wrap{
  position: relative;
  .small{
    position: absolute;
    top:0;
    left:0;
    img{
      width: 100%;
      height:100%;
      vertical-align: top;
    }
    .mask{
      position: absolute;
      background-color: rgba(0,0,0,0.4);
    }
  }
  .big{
    position: absolute;
    top:0;
    left:100%;
    overflow: hidden;
    img{
      position: absolute;
    }
  }
}
</style>
