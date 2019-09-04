<template>
  <div class="login">
    <h1>{{ msg }}</h1>
    <p>{{ oop }}</p>
    <form>
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text"></span>
        </div>
        <input type="text" v-model="username" class="form-control" placeholder="Username" id="uName" name="username">
      </div>
      <div class="input-group mb-3">
        <div class="input-group-prepend">
          <span class="input-group-text"></span>
        </div>
        <input type="text" v-model="password" class="form-control" placeholder="Password" id="uPwrd" name="Password">
      </div>
      <button type="submit" v-on:click="post" class="btn btn-primary">&nbsp;&nbsp;登录&nbsp;&nbsp;</button>
    </form>
  </div>
</template>
<script src="https://cdn.staticfile.org/vue/2.4.2/vue.min.js"></script>
<script src="https://cdn.staticfile.org/axios/0.18.0/axios.min.js"></script>
<script>
  import {baseURL} from '../api/config'

  export default {
    name: 'LogIn',
    data () {
      return {
        msg: '登录',
        oop: null
      }
    },
    methods: {
      oop: function(url,map){
        alert("666")
      },
      post: function () {
        /*this.postAxios('/loginUser',{
          username: this.username,        // 参数 firstName
          password: this.password
        }).then((data)=>{
          alert('测试回调'+data.data.usernameBase64)
        })*/
        axios.post(baseURL+'/loginUser', {
          username: decodeURI(this.username),        // 参数 firstName
          password: decodeURI(this.password)    // 参数 lastName
        })
          .then(function (response) {
            alert(response.data.usernameBase64)
            if (response.status === 200){
              alert("通过");
              axios.post(baseURL+'/loginUser', {        // 登录成功后跳转主页
                username: decodeURI(this.username),        // 参数 firstName
                password: decodeURI(this.password)    // 参数 lastName
              })
                .then(function (response) {
                  if (response.status === 200){
                    alert("通过")
                    // window.location.href = "http://localhost:8081/#/Orp"
                  }
                  alert('状态码是：'+response.status)
                  console.log(response)
                })
                .catch(function (error) {
                  console.log(error)
                })
            }
            alert('状态码是：'+response.status)
            console.log(response.usernameBase64)
          })
          .catch(function (error) {
            console.log(error)
          })
      }
    }
  }
</script>

<style scoped>

</style>
