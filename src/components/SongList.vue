<template>
    <div>
        <div v-if="!isPlayerVisisble">
            <div class="title font-bold text-center text-3xl mb-7 mt-3">
                <h1>Vue Music App</h1> 
                <img src="logo.png"/>
            </div>
            <div 
                v-for="(song, songIndex) in list" v-bind:key="song.id" 
                class="hover flex flex-row justify-between mb-4 cursor-pointer"
                v-on:click="selectSong(songIndex)"
            >
                <div class="word">
                    <span class="text-yellow-300">{{song.name}}</span>
                    <br/>
                    <span class="text-gray-100 text-xs">
                        {{song.artistName}} -
                        <span class="text-gray-200">
                            {{song.albumName}} 
                            {{song.year}}
                        </span>
                    </span>
                </div>
                <div>
                    <img
                    class="max-h-12 rounded" 
                    v-bind:src="song.src"/>
                </div>
            </div>
        </div>
        <div v-if="isPlayerVisisble">
            <SongPlayer
                v-bind:song="list[currentSongIndex]"
                @goback="isPlayerVisisble = !isPlayerVisisble"
                @next="playNext"
                @previous="playPrevious"
            />
        </div>
    </div>
</template>

<script>
import SongPlayer from './SongPlayer.vue';

export default {
    data() {
        return {
            isPlayerVisisble: false,
            currentSongIndex: 0,
            list: [
                {
                    id: 1,
                    name: 'Cheap Thrills',
                    artistName: 'Adam Lambert',
                    albumName: 'Everything',
                    year: 2021,
                    src: `https://images.pexels.com/photos/2858374/pexels-photo-2858374.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940`,
                    songSrc: `https://file-examples-com.github.io/uploads/2017/11/file_example_MP3_700KB.mp3`
                },
                {
                    id: 2,
                    name: 'Lean on',
                    artistName: 'Adam Levine',
                    albumName: 'Goind Down',
                    year: 2001,
                    src: `https://images.pexels.com/photos/6842724/pexels-photo-6842724.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500`,
                    songSrc: `https://filesamples.com/samples/audio/mp3/sample3.mp3`
                },
                {
                    id: 3,
                    name: 'Counting Stars',
                    artistName: 'Adam Hart',
                    albumName: 'Spice It Up',
                    year: 2013,
                    src: `https://images.pexels.com/photos/5995324/pexels-photo-5995324.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940`,
                    songSrc: `https://filesamples.com/samples/audio/mp3/sample1.mp3`
                }
            ]
        }
    },
    methods: {
        selectSong (index) {
            this.currentSongIndex = index;
            this.isPlayerVisisble = true;
        },
        playNext () {
            if(this.currentSongIndex < this.list.length - 1){
                this.currentSongIndex += 1;
            } else {
                this.currentSongIndex = 0;
            }
        },
        playPrevious () {
            if(this.currentSongIndex != 0) {
                this.currentSongIndex -= 1;
            } else {
                this.currentSongIndex = this.list.length - 1;
            }
        },
    },
    components: {
        SongPlayer
    },
    name: 'SongList'
}
</script>
