<template>
  <div id="search">
      <h1>Search GitHub Users</h1>
      <div id="submit">
        <input 
        type="text" 
        placeholder="username"
        v-model="keyword">
        <button @click="submit">Submit</button>
      </div>
  </div>
</template>

<script>
import axios from 'axios'
    export default {
        name:'Search',
        data() {
            return {
                keyword:''
            }
        },
        methods:{
            submit(){
                //提交时的数据状态
                 this.$bus.$emit('getUsers',{
                            isFirst:false,
                            isLoading:true,
                            users:[],
                            errorMesg:''
                        })
                        
                axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
                    //得到结果后的数据状态
                    response=>{
                        
                        this.$bus.$emit('getUsers',{
                            isFirst:false,
                            isLoading:false,
                            users:response.data.items,
                            errorMesg:''
                        })
                    },
                    //错误后的数据状态
                    error=>{
                        this.$bus.$emit('getUsers',{
                            isFirst:false,
                            isLoading:false,
                            users:[],
                            errorMesg:error.message
                        })
                    }
                )
            }
        }
    }
</script>

<style>
    div#submit{
        line-height: 60px;
        width: 400px;
        margin:0 auto;
        text-align: center;
    }
    input{
        border: 1px solid gray;
        border-radius: 5px;
        width: 250px;
        height: 30px;
        padding-left: 6px;
        font-size: 13px;
    }
    button{
        box-sizing: content-box;
        height: 30px;
        width: 50px;
        border: 1px solid gray;
        border-radius: 5px;
        padding: 1px 5px;
        margin-left: 5px;
        cursor: pointer;
    }
    button:hover{
        /* background-color: rgb(185, 185, 185); */
        outline: black 1px solid;
    }
    button:active{
        background-color: white;
    }
</style>