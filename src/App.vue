<template>
<div >
  
  <div class="container">
    <navbar-page/> 
   
    <h1 class="title">Youtube Demo</h1>
    <search-bar @termChange="onTermChange"/>
    <div class="detailDiv">
      <video-detail :video="selectedVideo"/>
      <video-list @videoSelect="onVideoSelect" :videos="videos"/>
    </div>
    </div>
   
</div>

</template>

<script>
import NavbarPage from './components/NavbarPage.vue'
import SearchBar from './components/SearchBar.vue'
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    NavbarPage,
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      videos:[],
      selectedVideo:null
    }
  },
  methods:{
  onTermChange(searchTerm){
    axios.get('https://www.googleapis.com/youtube/v3/search',{
      params:{
        part:'snippet',
        type:'video',
        key:'AIzaSyB3BpYEmvKrmRbQ1RyKz9pwBAST7V_lezE',
        q:searchTerm
      }
    })
    .then(response =>{
      console.log(response);
      this.videos = response.data.items;
    })
    .catch(err=>console.error(err.message))
  },
  onVideoSelect(video){
    this.selectedVideo = video;

  }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
.container{
  max-width: 1200px;
  width: 100%;
  margin: 50px auto;
  margin-top: 100px;
}
.title{
  text-align: center;
}
form{
  display: flex;
  margin: 20px 0px;
}
input{
  width: 85%;
  padding: 8px;
  margin-right: 20px;
  border-radius: 20px;
}
button{
  width: 15%;
  border: none;
  background: green;
  color: white;
  font-size: 18px;
  border-radius: 20px;
  cursor:pointer
}
.detailDiv{
  display: flex;
}
/* Tarayıcı varsayılan stillerini sıfırlıyoruz */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}

/* Arka plan resmini ayarlıyoruz */
#app {
  min-height: 100%;
  background-image: url('@/assets/ultra.jpg'); /* Resminizin doğru yolunu belirtin */
  background-size: cover;       /* Resmi alanı kaplayacak şekilde ölçeklendirir */
  background-repeat: no-repeat; /* Resmin tekrar etmesini engeller */
  background-position: center;  /* Resmi ortalar */
  position: relative;           /* Üstteki bileşenlerin doğru konumlandırılması için */
}
</style>

