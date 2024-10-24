<script setup>
// Import
  import { onMounted, reactive } from 'vue';

  const messages = reactive({
    values: []
  });

  onMounted(() => {
    fetch('https://zero3-challenge-mongodb-api.onrender.com/api/v1/messages/')
      .then(response => response.json())
      .then(data => {
        // console.log(data);
        messages.values = data.data.messages;
        // console.log(messages.values)
      });
  });

</script>

<template>
  <h1>Comment</h1>
  <ul>
    <li v-for="message in messages.values" :key="message._id">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>

</style>
