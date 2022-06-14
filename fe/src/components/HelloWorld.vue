<template>
  <div class="Blog">
    <input
    v-model = "userId"
    type = "text">
    <input
    v-model = "username"
    type="text">
    <button
    @click="postBlog"
    >POST</button>
    <button
    @click="getBlog">GET</button>
<div 
v-for="user in userPost"
:key = "user in userId">

  <h1>{{user.username}}</h1>
    {{user.userPost}} 
</div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data(){
  return{
    userId:[],
    username : [],
    userPost : []
}
},
methods:{
  postBlog(){
    console.log("Running a post");
    axios.request({
      url:"http://127.0.0.1:5000/api/post",
      method:"POST",
      data:{
        username:this.username,
        userId:this.userId
      }
    }).then(()=>{
      this.getBlog();
    }).catch((error)=>{
      console.log(error);
    })
  },
  getBlog(){
    console.log("Running a GET");
    axios.request({
      url:"http://127.0.0.1:5000/api/post",
      method:"GET"
    }).then((response)=>{
      console.log(response);
     this.userPost=response.data
    }).catch((error)=>{
      console.log(error);
    }).finally
  }

},
mounted (){
  this.getPosts
}
}



</script>
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
