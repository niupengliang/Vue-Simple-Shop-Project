<template>
  <div class="nav-bar" :class="{'is_fixed':isFixed}">
    <div class="container">
      <div class="pro-title">
        {{title}}
      </div>
      <div class="pro-param">
        <a href="">概述</a><span>|</span>
        <a href="">参数</a><span>|</span>
        <a href="">用户评价</a><span></span>
        <el-button type="danger" size='mini' @click="buy">立即购买</el-button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'nav-bar',
    props:{title:String},
    data(){
      return{
          isFixed:false
      }
    },
    mounted(){
      window.addEventListener('scroll',this.initHeight)
    },
    methods:{
      initHeight(){
        let scrollTop=window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop
        this.isFixed=scrollTop>151?true:false;
      },
      buy(){
        let {id} = this.$route.params;
        this.$router.push(`/detail/${id}`)
      }
    },
    destroyed(){
      window.removeEventListener('scroll',this.initHeight,false)
    }
  }
</script>

<style lang="scss" scoped>
@import './../assets/scss/config.scss';
@import './../assets/scss/mixin.scss';
.nav-bar{
  height:70px ;
  line-height: 70px;
  border-top: 1px solid #E5E5E5;
  background-color: #fff;
 
  &.is_fixed{
    position: fixed;
    top: 0;
    width: 100%;
     box-shadow: 0 5px 5px $colorE;
  }
  .container{
      display: flex;
      justify-content: space-between;
    .pro-title{
      font-size: 18px;
      color:$colorB;
      font-weight: bold;
    }
    .pro-param{
        font-size: 14px;
        // color: $colorC;
        a{
          color: $colorC;
        }
        span{
          margin: 0 5px;
        }

      }
  }
}
</style>