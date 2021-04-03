<template>
  <div id="app">
   <router-view></router-view>
  </div>
</template>

<script>
  import { mapActions } from 'vuex';

export default {
  name: 'App',
  data(){
    return {

    }
  },
  mounted(){
    this.getUser(),
    this.getCartCount();
  },
  methods:{
    getUser(){
       this.axios.get('/user').then((res)=>{
        //to-do保存到vuex中
        // this.$store.dispatch('saveUserName',res.username)
        this.saveUserName(res.username);
      })
    },
    getCartCount(){
      this.axios.get('/carts/products/sum').then((res)=>{
        // this.$store.dispatch('saveCartCount',res)
        this.saveCartCount(res)
      })
    },
    ...mapActions(['saveUserName','saveCartCount'])
  },
  
}
</script>

<style>
@import './assets/scss/reset.scss';
</style>
