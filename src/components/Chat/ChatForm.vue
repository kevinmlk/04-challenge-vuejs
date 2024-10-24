<script setup>
import { ref } from 'vue';

const messageInput = ref('');
// Define the 'sendMessage' event
const emit = defineEmits(['sendMessage']);

function doit() {
  console.log("Message Input Value:", messageInput.value);

  const newMessage = {
    user: "Kevin",
    text: messageInput.value,
  };

  if (!messageInput.value.trim()) {
    console.warn("Message cannot be empty.");
    return;
  }

  fetch('https://zero3-challenge-mongodb-api.onrender.com/api/v1/messages/', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newMessage),
  })
  .then(response => response.json())
  .then(data => {
    if (data.status === 'success') {
      // Emit the event with the new message data
      emit('sendMessage', data.data.message);
      // Clear the input field
      messageInput.value = '';
    } else {
      console.error("Error: ", data);
    }
  })
  .catch(error => {
    console.error("Error posting message:", error);
  });
}
</script>

<template>
  <div class="form">
    <input v-model="messageInput" type="text" placeholder="Write a message..." />
    <button @click="doit">Send</button>
  </div>
</template>

<style scoped>
/* Add any necessary styling here */
</style>
