<script setup>
import { onMounted, reactive } from 'vue';
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
  <ChatMessages :messages="messages.values" />
  <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>
/* Add any necessary styling here */
</style>
