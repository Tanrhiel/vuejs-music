<template>
  <div class="flex">
    <div class="flex-auto">
      <div class="p-6 max-w-xl mx-auto bg-white rounded-xl shadow-md flex items-center space-x-4">
        <div class="flex-shrink-0">
          <img class="h-12 w-12" src={{current.image}} alt="Album">
        </div>
        <div>
          <h2 class="text-blue-600 md:text-green-600 ">{{ current.title }} <span>{{ current.artist }}</span></h2>
          <div class="flex">
            <span class="flex-1"> <i class="fas fa-arrow-circle-left md:text-green-600"></i> </span>
            <span class="flex-1"> <i class="fas fa-play-circle md:text-green-600" v-if="!isPlaying" @click="play"></i> </span>
            <span class="flex-1"> <i class="fas fa-pause-circle md:text-green-600" @click="pause" ></i> </span>
            <span class="flex-1"> <i class="fas fa-arrow-circle-right md:text-green-600"></i> </span>
          </div>
        </div>
      </div>          

    </div>
    <div class="flex-1">
      <div class="p-6 max-w-xl mx-auto bg-white rounded-xl shadow-md flex items-center space-x-4">
        <div>
          <h2 class="text-blue-600 md:text-green-600 ">PlayList</h2>
          <p v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing':'song'">
            {{ song.title }} - <span>{{ song.artist }}</span>
          </p>            
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import Nav from './components/Nav.vue'

export default {
  name: 'App',
  data(){
    return{
      current:{},
      index:0,
      isPlaying: false,
      songs:[
        {
        title: 'Trouble Scene',
        artist: 'MWD',
        src: require('./assets/songs/musics/music_397.mp3'),
        image:require('./assets/songs/images/vinyl.jpeg'),
      },
      {
        title: 'A little Christmas music',
        artist: 'Lena Orsa',
        src: require('./assets/songs/musics/music_397.mp3'),
        image:require('./assets/songs/images/lenaOrsa.jpeg')
      },
      ],
      player:new Audio()
    }
  },
  methods:{
    play(song){
      if(song.src !="undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
