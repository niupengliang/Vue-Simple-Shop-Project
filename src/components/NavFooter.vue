<template>
  <div class="footer">
    <div class="footer-logo">
      <img src="/imgs/logo-footer.png" alt="">
      <p>小米商城</p>
    </div>
    <div class="footer-link">
      <a href="https://www.mi.com/" target="_blank">小米主页</a><span>|</span>
      <a href="https://cn.vuejs.org/" target="_blank">Vue全栈</a><span>|</span>
      <a href="http://nav.react-china.org/" target="_blank">React全家桶</a><span>|</span>
      <a href="" target="_blank">微信支付专项</a>
      <div class="copyright" >copyright 2019<span>mi.futurefe.com</span>All right Result for mi-mall</div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'nav-footer'
  }
</script>

<style lang="scss" scoped>
.footer{
  @import '../assets/scss/config.scss';
  height: 234px;
  border-top: 4px solid $colorA;
  background-color: #333333;
  color:#999999;
  font-size: $fontI;
  text-align: center;
  .footer-logo{
    margin-top: 46px;
    margin-bottom: 31px;
    img{  
    width: 53px;
    height: 36px;
    margin-bottom:13px ;
    }
  }
      .footer-link{
        a{
          color: #999999;
          display:inline-block;
        }
        span{
          margin:0 10px 0 10px ;
        }
        .copyright{
          span{
            color: $colorA;
          }
        }
    }
}
</style>