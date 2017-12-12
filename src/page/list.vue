<template>
  <div style="margin: 50px 0">
    <ol>
      <li class="list" v-for="item of msg" :key='item.length'>
        <div style="flex: 1">
          <img :src="item.author.avatar_url" alt="">
        </div>
        <div class="font" style="flex: 8">
          <p class="title">
            {{item.title}}
          </p>
          <p class="time">
            {{Time(item.create_at)}}
          </p>
        </div>
      </li>
    </ol>

  </div>
</template>
<script>
  export default{
    data:function(){
      return {
        number:10,
        msg:[],
      }
    },
    props:{
      page:{
        type:Number,
        default:1
      },
      fin:{
        type:Boolean,
        default:true
      }
    },
    methods:{
      songdata(){
        let _this = this
        _this.$http.get('https://cnodejs.org/api/v1/topics', {
          params:{
            page: _this.page,
            limit: this.number,
            mdrender: 'false'
          }
        }).then(function (res) {
          //_this.msg = _this.msg.concat(res.data.data)//连续加载
          _this.msg=res.data.data;//翻页加载
            //console.log(res)
          setTimeout(function () {
            _this.fin=true;
          },500)
        })
      },
      Time(time) {
        return String(time).match(/.{10}/)[0]
      },
    },
    mounted(){
      this.songdata()
    },
    watch:{
      page(val,oldval){
        this.songdata()
      }
    }
  }
</script>
<style>
  .list li{
    margin: 0px 0 6px 0;
    display: flex;
    height: 100px;
    font-size: 16px;
    background: #e2e2e2;
    color: #222;
    margin-left: -40px;
  }
  .list img{
    height: 80px;
   margin-top: 10px;
  }
  .title{
    box-sizing: border-box;
    padding: 6px 0 20px 20px;
    width:100%;
    display: -webkit-box;
    -webkit-line-clamp: 1;
    -webkit-box-orient: vertical;
    overflow: hidden;
    height: 20px;
    text-align: left;
    margin-bottom: 20px;
  }
  .time{
    padding-left:20px ;
    text-align: left;
  }
  .font{

  }
</style>
