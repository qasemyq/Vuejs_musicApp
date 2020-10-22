<template>
  <div id="app">
    <header>
      <h1>GG Music</h1>
    </header>
    <main>
      <section class="player">
        <!-- har chi tu payin tu gesmate data change beshe inja ham dide mishe  -->
        <!-- inja bayd - bezaram -->
        <h2 class="song-title ">{{current.title}} - <span>{{current.singer}}</span></h2>
        <!-- inja mikham bara app control bezaram -->
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <!--inja migam if not isplaying-->
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <!-- inja ham v-else mizaram ke bala bara play v-ifesho gozashtam  -->
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
        </section>
        <section class="playlist">
          <h3>The playlist</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">{{song.title}} - {{song.singer}}</button>
        </section>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data (){
    return {
     current: {
     },
     index: 0, 
     // ye motagayer misazam bar bara isplaying va false mizaram 
     isPlaying: false,
     songs: [
       {
         title: "what you gonna do",
         singer: "Jastin",
         // injuri ba require mitunam song haye ke tu asset hast ro be dast biyaram 
         src: require('./assets/JustinBieber.mp3')
       },
       {
         title: "JH",
         singer: "Gmizi",
         // injuri ba require mitunam song haye ke tu asset hast ro be dast biyaram 
         src: require('./assets/111.mp3')
       }
     ],
     // ba in mitunam audio ro dakhele appemun handel konam 
     player: new Audio()
    }
  },
  // inja mikham biyam va function hamuno benevisam 
  methods: {
    play(song) {
      // age typeofe song.src mosavi nabud ba undefined  
      if(typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    },
    prev () {
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index]
      this.play(this.current)
    },
  },
  // be mahze inke app sakhte shod inro ejra mikonim 
  created (){
    // this inja data hast, index ro bala tarif mikonam va 0 ro behesh midam 
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // inja vagti ino minevisam play mikone 
    //this.player.play();
  }
  
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: sans-serif;
  }
  header {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: #212121;
    color: #fff;
  }
  main {
    width: 100%;
    max-width: 768px;
    margin: 0 auto;
    padding: 25px;
  }
.song-title {
  color: skyblue;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}

.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
   justify-content: center;
   align-items: center;
   padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none ;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play, .pause {
  font-size:  20px;
   font-weight: 700;
   padding: 15px 25px;
   margin: 0px 15px;
   border-radius: 8px;
   color: #fff;
   background-color: tomato;
}
.next, .prev {
  font-size:  16px;
   font-weight: 700;
   padding: 10px 20px;
   margin: 0px 15px;
   border-radius: 6px;
   color: #fff;
   background-color: rgb(233, 65, 35);
}
.playlist {
  padding: 0px 30px;
}

.playlist h3 {
   color: #212121;
   font-size: 28px;
   font-weight: 400;
   margin-bottom: 30px;
   text-align: center;
}

.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px ;
  font-weight: 700;
   cursor: pointer;
}
.playlist .song:hover {
  color: tomato;
}
.playlist .song.playing {
  color: white;
  background: tomato;

}
</style>
