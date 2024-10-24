<script setup>
  const props = defineProps({
    videosrc: String
  })
</script>

<template>
  <div class="player">
    <video autoplay muted loop :src="videosrc"></video>
    <div class="player__controls">
      <a href="#" @click.prevent="$emit('prev-video')">🆙</a>
      <a href="#" @click.prevent="$emit('next-video')">🆗</a>
    </div>
  </div>
</template>

<style scoped>
  video {
    max-height: 100vh;
  }

  .player {
    background-image: url('/thumb.png');
    background-repeat: no-repeat;
    background-size: cover;
    display: flex;
    justify-content: center;
  }

  .player__controls {
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
</style>
