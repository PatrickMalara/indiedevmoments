<template>
  <div id="app" class="container-fluid">
    <div class="row">
      <div v-for="post in posts" :key="post.url" class="col-2 m-2">
          {{post.title}}
          <img :src="post.imgUrl" style="width: 100%; height:256px; object-fit:cover;">
      </div>
    </div>
    <a href="#" @click="getdata">Click me</a>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/database";

var config = {
        apiKey: "AIzaSyDDbdhDzdsHD7gkbUh8c0iwYVqYdttMAAk",
        authDomain: "indiedevmoments-4f851.firebaseapp.com",
        databaseURL: "https://indiedevmoments-4f851.firebaseio.com",
        projectId: "indiedevmoments-4f851",
        storageBucket: "indiedevmoments-4f851.appspot.com",
        messagingSenderId: "386841054125",
        appId: "1:386841054125:web:913a8fc07163bb86106f24"
};
firebase.initializeApp(config);
const database = firebase.database();
export default {
name: 'App',
components: {
     
},
data(){
    return{
      posts: []
    };
},
methods: {
  getdata(){
    var ref = database.ref('/posts/');
    ref.on("value", (snapshot) => {
      this.posts = snapshot.val();
    });
  }
},
mounted(){
  this.getdata();
  console.log(this.posts);
}
}
</script>

<style>
</style>
