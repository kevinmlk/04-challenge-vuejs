<script setup>
  import { ref } from "vue";

  // Ref to store the input message
  const messageInput = ref("");
  
  console.log(messageInput);

  function doit() {
    // Create a new message object
    const newMessage = {
      user: "Kevin", // Replace with actual user data if available
      text: messageInput.value,
    };

    // Make sure the input value is not empty before sending the request
    if (!messageInput.value.trim()) {
      console.warn("Message cannot be empty.");
      return;
    }

    // Send a POST request to the API
    fetch('https://zero3-challenge-mongodb-api.onrender.com/api/v1/messages/', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newMessage),
    })
    .then(response => response.json())
    .then(data => {
      if (data.status === "success") {
        // Emit the new message to the parent component
        emit("sendMessage", data.data.message);
        // Clear the input field
        messageInput.value = "";
      }
    })
    .catch(error => {
      console.error("Error posting message:", error);
    });
  }
</script>

<template>
  <div class="form">
    <h3></h3>
    <ul>
      <li>
        <span class="name"></span>
        <span class="message"></span>
      </li>
    </ul>
    <input v-model="messageInput" type="text" placeholder="Write a message..." />
    <button @click="doit">Send</button>
  </div>
</template>

<style scoped>

</style>
