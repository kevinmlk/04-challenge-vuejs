<script setup>
  import { onMounted, ref, reactive } from 'vue';
  // Import components
  import VideoPlayer from './components/Video/VideoPlayer.vue';
  import VideoDetails from './components/Video/VideoDetails.vue';
  import Chat from './components/Chat/Chat.vue';

  const currentTitle = ref('Some title here');
  const currentVideo = ref('');
  const videos = reactive({
    values: []
  });
  const currentVideoIndex = ref(0);

  onMounted(() => {
    fetch('https://api.jsonbin.io/v3/b/670ccbfaad19ca34f8b81951/')
      .then(response => response.json())
      .then(data => {
        videos.values = data.record.data.videos;
        currentVideo.value = data.record.data.videos[0].video;
        currentTitle.value = data.record.data.videos[0].description;
      });
  });

  function nextVideo() {
    currentVideoIndex.value++;
    if (currentVideoIndex.value >= videos.values.length) {
      currentVideoIndex.value = 0;
    }
    currentVideo.value = videos.values[currentVideoIndex.value].video;
    currentTitle.value = videos.values[currentVideoIndex.value].description;
  }

  function prevVideo() {
    currentVideoIndex.value--;
    if (currentVideoIndex.value < 0) {
      currentVideoIndex.value = videos.values.length - 1;
    }
    currentVideo.value = videos.values[currentVideoIndex.value].video;
    currentTitle.value = videos.values[currentVideoIndex.value].description;
  }

</script>

<template>
  <div class="grid">
    <!-- Video player -->
    <div class="player">
      <VideoPlayer @prevVideo="prevVideo" @nextVideo="nextVideo" :videosrc="currentVideo" />
    </div>
    <!-- Chat messages -->
    <div class="messages">
      <!-- Video details -->
      <VideoDetails :title="currentTitle" />
      <!-- Chat form -->
      <Chat />
    </div>
  </div>
</template>

<style scoped>
  .grid {
    font-family: Helvetica, sans-serif;
    display: grid;
    grid-template-columns: 2fr 2fr;

  }
</style>
