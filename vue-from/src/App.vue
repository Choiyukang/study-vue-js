<template>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">id: </label>
        <input type="text" id="username" v-model="username">
      </div>
      <div>
        <label for="password">pw: </label>
        <input type="password" id="password" v-model="password">
      </div>
      <button type="submit">login</button>
      <a v-on:click="getUsers">btn</a>
      <div>{{users}}</div>
    </form>
    
</template>

<script>
import axios from 'axios';

export default {
  data: function(){
    return{
      username:'',
      password:'',
      users:[]
    }
  },
  methods:{
    submitForm:function(){
      console.log(this.username,this.password);
      var url ='https://jsonplaceholder.typicode.com/users';
      var data = {
        username: this.username,
        password: this.password
      }
      axios.post(url,data)
      .then(function(response){
        console.log(response);
      })
      .catch(function(response){
        console.log(response);
      })
    },
    getUsers:function(){
      // var url1 = "http://localhost:63204/api/getusers";
      // var url2 = "/api/getusers";
      this.$axios.get('api/api/GetUsers')
      .then(function(response){
          console.log(response);
          console.log(response.data);
      })
      .catch(function(error){
        console.log(error);
      })

      // axios.get(url2)
      // .then(function(response){
      //     console.log(response);
      //     console.log(response.data);
      // })
      // .catch(function(error){
      //   console.log(error);
      // })
    }
  }
}
</script>

<style>

</style>