<template>
  <div class="xl:flex max-w-md mx-auto rounded-xl shadow-md overflow-hidden md:max-w-2xl">
    <div class="md:flex">
      <div class="max-w-md mx-auto bg-white rounded-xl shadow-md overflow-hidden md:max-w-2xl">
        <div class="md:flex-1 m-2">
          <div class="md:flex-shrink-0">
            <img class="h-48 w-full object-cover md:w-48" v-bind:src="current.image" alt="Album">
          </div>
          <div class="p-8">
            <div class="uppercase tracking-wide text-sm text-indigo-500 font-semibold">{{ current.title }} <span>{{ current.artist }}</span></div>
            <div class="flex">
                  <button class="flex-auto" @click="prev"> <i class="fas fa-arrow-circle-left md:text-green-600" ></i> </button>
                  <button class="flex-auto" v-if="!isPlaying" @click="play"> <i class="fas fa-play-circle md:text-green-600"></i> </button>
                  <button class="flex-auto" v-else @click="pause" > <i class="fas fa-pause-circle md:text-green-600"></i> </button>
                  <button class="flex-auto" @click="next"> <i class="fas fa-arrow-circle-right md:text-green-600"></i> </button>
                </div>
          </div>
        </div>
      </div>
      
    </div>          

    <div class="flex-1 m-2">
      <div class="md: p-6 max-w-xl mx-auto bg-white rounded-xl shadow-md items-center space-x-4">
        <div>
          <h2 class="text-green-600 sm:font-semibold text-8x1 md:font-bold">PlayList</h2>
          <hr class="m-2">
        </div>
        <div class="items-left">
          <button  v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing':'song'">
            {{ song.title }} - <span>{{ song.artist }}</span>
          </button>            
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
        image:'./assets/songs/images/vinyl.jpeg'
      },
      {
        title: 'A little Christmas music',
        artist: 'Lena Orsa',
        src: require('./assets/songs/musics/music_398.mp3'),
        image:'./assets/songs/images/lenaOrsa.jpeg'
      },
      ],
      player:new Audio()
    }
  },
  methods:{
    play(song){
      if(typeof song.src != "undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause(){
      this.player.pause();
      this.isPlaying = false;
    },
    prev(){
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next(){
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  
  }
}
</script>

<style>
body{
  background: linear-gradient(90deg, rgba(97,84,254,1) 0%, rgba(82,182,254,1) 100%);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
