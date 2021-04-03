<template>
  <div class="index">
    <div class="container">
      <div class="swiper-box">
        <div class="nav-menu">
          <ul class="menu-wrap">
            <li class="menu-item">
              <a href="javascript:;">手机 电话卡<i class="el-icon-arrow-right"></i></a>
                      <div class="children">
                          <ul v-for="item in menuList" :key="item.id">
                            <li v-for="sub in item" :key="sub.id">
                                <a :href="sub.id?'/#/product/'+sub.id:''"><img v-lazy="sub.img?sub.img:'/imgs/item-box-1.png'" alt="">{{sub.name?sub.name:'小米CC9'}}</a>
                            </li>
                          </ul>
                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">电视 盒子<i class="el-icon-arrow-right"></i></a>
                       <div class="children">

                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">笔记本 平板<i class="el-icon-arrow-right"></i></a>
                      <div class="children">

                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">家电 插线板<i class="el-icon-arrow-right"></i></a>
                       <div class="children">

                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">出行 穿戴<i class="el-icon-arrow-right"></i></a>
                       <div class="children">

                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">智能 路由器<i class="el-icon-arrow-right"></i></a>
                      <div class="children">

                      </div>  
            </li>
            <li class="menu-item">
              <a href="javascript:;">电源 配件<i class="el-icon-arrow-right"></i></a>
                      <div class="children">

                      </div>
            </li>
            <li class="menu-item">
              <a href="javascript:;">生活 箱包<i class="el-icon-arrow-right"></i></a>
                     <div class="children">

                      </div>
            </li>
          </ul>
        </div>

        <el-carousel trigger="click" height="460px" arrow="always" autoplay>
      <el-carousel-item v-for="item in slideList" :key="item.id">
        <a href=""><img :src="item.img" alt=""></a>
      </el-carousel-item>
    </el-carousel>
      </div>
      <div class="ads-box">
        <a href="'/#/product/'+item.id" v-for="item in adsList" :key="item.id"><img v-lazy="item.img" alt=""></a>
      </div>
      <div class="banner">
        <a href="'/#/product/30'">
          <img v-lazy="'/imgs/banner-1.png'" alt="">
        </a>
        </div>      
    </div>
      <div class="product-box">
        <div class="container">
          <h2>手机</h2>
        <div class="wrapper">
          <div class="banner-left">
            <a href="/#/product/35"><img src="/imgs/mix-alpha.jpg" alt=""></a>
          </div>
          <div class="list-box">
                      <div class="list" v-for="(arr,i) in phoneList" :key="i">
            <div class="item" v-for="(item,j) in arr" :key="j">
              <span :class="{'new-pro':j%2==0}">新品</span>
              <div class="item-img">
                <img v-lazy="item.mainImage" alt="">
              </div>
              <div class="item-info">
                <h3>{{item.name}}</h3>
                <p>{{item.subtitle}}</p>
                <p class="price">{{item.price | currency}} <i class="el-icon-shopping-cart-full" @click="open"></i></p>
              </div>
            </div>
          </div>
          </div>
        </div>
        </div>
        
      </div>
    <service-bar></service-bar>
  </div>
</template>

<script>  
import ServiceBar from '@/components/ServiceBar'
  export default {
    name:'index',   
    components:{
      ServiceBar
    },  
    data(){
      return{
        swiperOption:{  

        },
        slideList:[
          {
          img:'/imgs/slider/slide-1.jpg',
          id:'42'
        },
          {
          img:'/imgs/slider/slide-2.jpg',
          id:'45'
        },
          {
          img:'/imgs/slider/slide-3.jpg',
          id:'46'
        },
          {
          img:'/imgs/slider/slide-4.jpg',
          id:'47'
        },
          {
          img:'/imgs/slider/slide-5.jpg',
          id:'48'
        }
        ],
        menuList:[
          [
            {
              img:'/imgs/item-box-1.png',
              name:'小米CC9',
              id:30
            },
            {
              img:'/imgs/item-box-2.png',
              name:'小米8青春版',
              id:31
            },
            {
              img:'/imgs/item-box-3.jpg',
              name:'Redmi K20 Pro',
              id:32
            },
            {
              img:'/imgs/item-box-1.png',
              name:'移动4G专区',
              id:33
            }
          ],
          [1,2,3,4],
          [1,2,3,4],
          [1,2,3,4],
          [1,2,3,4],
          [1,2,3,4]
        ],
        adsList:[
          {
            id:33,
            img:'/imgs/ads/ads-1.png'
          },
          {
            id:48,
            img:'/imgs/ads/ads-2.jpg'
          },
          {
            id:45,
            img:'/imgs/ads/ads-3.png'
          },
          {
            id:17,
            img:'/imgs/ads/ads-4.jpg'
          }
        ],
        phoneList:[]
      }
    },
    mounted(){
      this.init();
    },
    methods:{
      init(){
        this.axios.get('/products',{
          params:{
            categoryId:100012,
            pageSize:14
          }
        }).then((res)=>{
          res.list = res.list.slice(6,14)
          this.phoneList=[res.list.slice(0,4),res.list.slice(4,8)]
        })
      },
       open() {
        this.$confirm('是否将该商品加入购物车？', '确认添加', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          // type: 'error'
        }).then(() => {
          this.$message({
            type: 'success',
            message: '商品添加成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消'
          });          
        });
      }

    },
    filters:{
      currency(val){
        if (!val) {
          return '0.00'
        }else{
          return '￥'+val.toFixed(2)+'元'
        }
      }
    }
  }

</script>

<style lang="scss">
@import './../assets/scss/base.scss';
@import './../assets/scss/mixin.scss';
@import './../assets/scss/config.scss';
.index{
  .container{
    .swiper-box{
      position: relative;
      .nav-menu{
        position:absolute;
        z-index: 10;
        width: 264px;
        height: 460px;
        padding:26px 0;
        background-color: #55585a7a;
        box-sizing: border-box;
        .menu-wrap{
          .menu-item{
            height: 50px;
            line-height: 50px;
            &:hover{
                background-color:$colorA;
                .children{
                  display: block;
                }
              }
            a{
              display: block;
              position: relative;
              font-size: 16px;
              color:#ffffff;
              padding-left: 30px;
              // &:after{
              //   position: absolute;
              //   right: 30px;
              //   top: 17.5px;
              //   content: '';
              //   display: block;
              //   @include bgImg(10px,15px,'/imgs/icon-arrow.png')
              // }
              i{
                position: absolute;
                right: 15px;
                top: 16px;
                font-size: 16px;
              }
              
            }
            .children{
              height:460px;
              width:962px;
              background-color: $colorG;
              position: absolute;
              top: 0;
              right: 0;
              left:264px;
              border: 1px solid $colorH;
              display: none;
              ul{
                display:flex;
                justify-content: space-between;
                height: 75px;
                li{
                  line-height: 75px;
                  height: 75px;
                  width: 241px;
                  padding-left: 23px;
                }
                a{
                  color: $colorB;
                  font-size: 14px;
                }
                img{
                  width: 32px;
                  height: 35px;
                  vertical-align: middle;
                  margin-right: 10px;
                }
              }
            }
          }
        }
      }
      .el-carousel__container{
        .el-carousel__arrow--left{
          left: 278px;
        }
        .el-carousel__item{
          a{
             img{
        // height: 460px;
        width: 100%;
      }
        }
        }
        
      }
           

        }
      }
      .ads-box{
        display:flex;
        justify-content: space-between;
        margin-top: 15px;
        margin-bottom: 31px;
        a{
          width: 296px;
          height: 167px;
          img{
            width:100%;
            height:100%;
          }
        }
      }
      .banner{
        width: 1226px;
        height: 120px;
        margin-bottom: 30px;
        a{
          width: 100%;
          height: 100%;
          img{
              width: 100%;
              height: 100%;
          }
        }
      }  
      .product-box{
        background-color: $colorJ;
        padding:30px 0 50px 0;
        h2{
            font-size: 22px;
            height: 21px;
            line-height: 21px;
            color: $colorB;
        }
        .wrapper{
          display:flex;
          .banner-left{
            margin-right: 16px;
            img{
            width: 224px;
            height: 619px;
            }
          }
        }
        .list-box{
          .list{
            display: flex;
            justify-content: space-between;
            width:986px;
            margin-bottom: 14px;
            &:last-child{
              margin-bottom: 0;
            }
            .item{
              width: 236px;
              height: 302px;
              background-color: $colorG;
              text-align: center;
              span{
                display: inline-block;
                width: 67px;
                height: 24px;
                font-size: 14px;
                color: #ffffff;
                line-height: 24px;
                &.new-pro{
                  
                background-color: #7ECF68;
                }
                &.kill-pro{
                background-color: #E82626;

                }
              }
              .item-img{

                img{
                  height: 160px;
                  width:80%;
                  padding-top: 10px;
                }
              }
              .item-info{
                h3{
                  font-size: $fontJ;
                  color: $colorB;
                  line-height: $fontJ;
                  font-weight: bold;
                }
                p{
                  color:$colorD;
                  line-height:13px;
                  margin: 6px 0 13px 0;
                }
                .price{
                  color:#F20A0A;
                  font-size: $fontJ;
                  font-weight: bold;
                  cursor: pointer;
                  i{
                    font-size: 16px;
                    margin-left: 3px;
                  }
                }
              }
            }
          }
        }
      }
    }

</style>