<template>
  <div class="app-container p-3 m-auto"> 
    <div class="overlay">
      <SongList/>
    </div>
  </div>
</template>

<script>
import SongList from './components/SongList.vue';

export default {
  name: 'App',
  components: {
    SongList
  }
}
</script>
