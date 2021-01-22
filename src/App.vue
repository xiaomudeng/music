<template>
  <div id="app">
    <div class="app-player">
      <!-- 1. 音乐盒顶部的开始 -->
      <div class="app-player-header">
        <my-music-header @getlist="handleGetMusicList"></my-music-header>
      </div>
      <!-- 1. 音乐盒顶部的结束 -->
      <!-- 2. 音乐盒中间内容开始 -->
      <div class="app-player-content">
        <my-music-content :song-list="songList" @geturl="handleGetSongUrl"></my-music-content>
      </div>
      <!-- 2. 音乐盒中间内容结束 -->
      <div class="app-player-footer" >
        <my-music-footer :song-url="songUrl"></my-music-footer>
      </div>
    </div>
  </div>
</template>

<script>
// import axios from "axios"
// window.axios = axios;
import MyMusicHeader from "@/components/my-music-header"
import MyMusicContent from "@/components/my-music-content"
import MyMusicFooter from "@/components/my-music-footer"
export default {
  name: "App",
  data:function(){
    return {
      songList:[],
      songUrl:"" // 歌曲的url
    }
  },
  components: {
    "my-music-header":MyMusicHeader,
    "my-music-content": MyMusicContent,
    "my-music-footer":MyMusicFooter
  },
  methods: {
    handleGetMusicList:function(songList){
      this.songList = songList;
    },
    handleGetSongUrl:function(songUrl){
      this.songUrl = songUrl;
    }
  },
};
</script>

<style>
#app {
  background: url(./assets/images/bg.jpeg) no-repeat;
  width: 100vw;
  height: 100vh;
  background-size: 100% 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  --themeColor: #1baad5;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.app-player {
  width: 800px;
  height: 600px;
  border-radius: 10px;
}
.app-player-header {
  height: 60px;
  width: 100%;
  background-color: var(--themeColor);
}
.app-player-content {
  height: 480px;
  width: 100%;
  display: flex;
  border-bottom: 1px dotted var(--themeColor);
  background-color: rgba(255, 255, 255, 0.5);
}

.app-player-footer {
  height: 60px;
  width: 100%;
  background-color: var(--themeColor);
}
</style>
