<template>
  <div>
    <audio v-bind:src="song.songSrc" preload="auto" autoplay ref="audioPlayer" />
    <div class="text-white">
      <div class="flex flex-row justify-between">
        <button class="stat__btn word" v-on:click="goback">Back</button>
        <div class=" title font-bold text-1xl">
          <img src="logo.png"/>
        </div>
      </div>
      <div class="word">
        <img class="rounded mt-4 mb-4" v-bind:src="song.src"/>
        <div class="text-center">
          <p class="text-yellow-300 font-bold">{{song.name}}</p>
          <p class="text-gray-200">{{song.artistName}} - {{song.albumName}}</p>
          <p class="text-gray-400">{{song.year}}</p>
        </div>
      </div>
        <div class="grid grid-cols-3 mt-10">
          <div class="flex item-center justify-center">
            <button class="stat__btn" v-on:click="previous">&#10094;&#10094;</button>
          </div>
          <div class="flex item-center justify-center"> 
            <button
              class="play__btn word rounded-full h-20 w-20 text-black font-bold"
              v-on:click="togglePlay"
            >
              {{ isPlaying ? 'Pause' : 'Play' }}
            </button>
          </div>
          <div class="flex item-center justify-center">
            <button class="stat__btn" v-on:click="next">&#10095;&#10095;</button>
          </div>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isPlaying: true
    }
  },
  name: 'SongPlayer',
  props: {
    song: {
        id: Number,
        name: String,
        artistName: String,
        albumName: String,
        year: Number,
        src: String,
        songSrc: String
    },
  },
  emits: ['goback','next','previous'],
  methods: {
    goback() {
      this.$emit('goback');
    },
    next() {
      this.$emit('next');
    },
    previous() {
      this.$emit('previous');
    },
    togglePlay() {
      if (this.isPlaying) {
        this.$refs.audioPlayer.pause();
      } else {
        this.$refs.audioPlayer.play();
      }
      this.isPlaying = !this.isPlaying;
    }
  }
}
</script>
