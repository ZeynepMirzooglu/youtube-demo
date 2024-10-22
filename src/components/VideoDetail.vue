<template>
  <div v-if="video" class="selectedVideoContainer">
    <div>
        <iframe class="selectedVideo" :src="videoUrl"></iframe>
    </div>
    <div class="details">
        <h4>{{video.snippet.tittle}}</h4>
        <p>{{video.snippet.description}}</p>
    </div>
  </div>
</template>

<script>
export default {
props:['video'],
computed:{
    videoUrl(){
        const {videoId}= this.video.id;
        return `https://www.yotube.com/embed/${videoId}`
    }
}
}
</script>

<style scoped>
.selectedVideoContainer{
    width: 100%;
}
.selectedVideo{
    width: 100%;
    height: 250px;
}
.details{
    border: 1px solid grey;
    border-radius: 4px;
    padding: 10px;
    margin-top: 10px;
}
</style>