<template>
  <div id="list">
      <div 
      class="item" 
      v-for="user of userObj.users " 
      :key="user.login"
      v-show="userObj.users.length"
      >
          <a href="user.html_url">
              <img :src="user.avatar_url" alt="">
          </a>
          <span>{{user.login}}</span>
      </div>
      <h2 v-show="userObj.isFirst">welcome to use</h2>
      <h2 v-show="userObj.isLoading">loading</h2>
      <h2  v-show="userObj.errorMesg">{{userObj.errorMesg}}</h2>
  </div>
</template>

<script>
    export default {
        name:'List',
        data(){
            return{
                //将github用户信息和搜索状态封装为一个对象
                userObj:{
                    users:[],
                    isFirst:true,
                    isLoading:false,
                    errorMesg:''
                }
            }
        },
        mounted(){
            //利用全局事件总线向Search组件拿userObj
            this.$bus.$on('getUsers',(userObj)=>{
                this.userObj=userObj
            })
        }
    }
</script>

<style>
    div#list{
        width: 1000px;
        margin: 12px auto 0px;
        text-align: center;
    }
    div.item{
        width: 198px;
        float: left;
        text-align: center;
        border: 1px solid rgb(223, 223, 223);
        
    }
    a{
        display: block;
    }
    div.item img{
        width: 180px;
    }
    div.item span{
        font-size: 14px;
    }
</style>