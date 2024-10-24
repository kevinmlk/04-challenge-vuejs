<script setup>

  const props = defineProps({
    messages: {
      type: Array,
      required: true
    }
  });

</script>

<template>
  <h1>Comment</h1>
  <ul>
    <li v-for="(message, index) in messages" :key="index">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>

</style>
