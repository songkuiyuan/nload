
<template>

  <div id="app">
    <a class="head" @click="prev">向上：第{{page}}页</a>
    <transition name="fade" mode="out-in">
        <list class="list" :page="page" :trigger.sync="fin"></list>
    </transition>
    <a class="footer" @click="next">向下：第{{page}}页</a>
    <div id="loader" v-show="!fin" :transition="up? 'up-start':'down-start'">
      <span>Loading</span>
    </div>
  </div>

</template>

<script>
  import list from '@/page/list';

export default {
  name: 'app',
  components:{
    list
  },
  data(){
    return {
      page:1,
      fin:true,
      up:false,
    }
  },
  methods:{
    prev(){
      let _this=this;
      if(_this.page==1){
        alert('已经是第一页了！')
      }else{
        _this.page--;
        _this.fin=false;
        _this.up=true;
        document.body.scrollTop = document.body.scrollHeight;
      }
    },
    next(){
      let _this=this;
      _this.page++;
      _this.fin=false;
      _this.up=false;
      document.body.scrollTop=0;
      document.documentElement.scrollTop=0;
    }
//    scrollMethod() {
//      let _this=this;
//      const sumH = document.body.scrollHeight;//body的高度
//      console.log(_this.page)
//      const viewH = document.documentElement.clientHeight;//页面可见区域的高
//      const scrollH = document.body.scrollTop;//body滚动的高度
//      if (viewH + scrollH === sumH) {
//        _this.page++;
//        console.log(_this.page)
//      }
//    },
  },
//  mounted() {
//    window.addEventListener('scroll',this.scrollMethod);
//  },
  watch: {
    fin (val, oldVal) {
      if (!oldVal && val && this.up) {
        document.body.scrollTop = document.body.scrollHeight;
        document.documentElement.scrollTop=document.documentElement.scrollHeight;
      }
    },

  }
}
</script>

<style scoped>
  html, body {
    height: 100%;
  }
  .button span {
    margin-left: 2em;
    font-size: .5rem;
    color: #d6d6d6;
  }
  #loader {
    width: 100%;
    min-height: 3em;
    position: fixed;
    left: 0;
    background: #212121;
    color: #fff;
  }
  #loader span {
    display: block;
    width: 100%;
    text-align: center;
    position: absolute;
    top: 50%;
    margin-top: -0.5em;
  }



  *{
    margin: 0;
    padding: 0;
  }
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
  .head{
    position: fixed;
    top:0;
    left: 0;
  }
  .footer{
    position: fixed;
    bottom: 0;
    left: 0;
  }
  .list{
    margin: 50px 0;
  }
  .head,.footer{
    display: block;
    background: #000;
    font-size: 16px;
    color:#fff;
    height: 50px;
    width: 100%;
    line-height: 50px;
    text-decoration: none;
  }
  #loader {
    width: 100%;
    min-height: 3em;
    position: fixed;
    left: 0;
    background: #212121;
    color: #fff;
  }
</style>
