<script setup>
  import { onMounted, reactive } from 'vue';
  // Import components
  import ChatMessages from './ChatMessages.vue';
  import ChatForm from './ChatForm.vue';

  const messages = reactive({
    values: []
  });
  

  onMounted(() => {
    fetch('https://zero3-challenge-mongodb-api.onrender.com/api/v1/messages/')
      .then(response => response.json())
      .then(data => {
        messages.values = data.data.messages;
    });
  });

  function addMessage(newMessage) {
    // Add the new message to the top of the list
    messages.values.unshift(newMessage);
  }
</script>

<template>
  <!-- Chat messages -->
  <ChatMessages />
  <!-- Chat form -->
  <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>

</style>
