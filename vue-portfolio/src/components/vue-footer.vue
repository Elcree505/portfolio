<template>
    <footer>
      <p>&copy; {{ currentYear }} Charles Lee. All rights reserved.</p>
    </footer>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const currentYear = ref(new Date().getFullYear());
  </script>
  
  <style scoped>
  footer {
    text-align: center;
    padding: 20px;
    background-color: var(--primary-color);
    color: var(--accent-color);
    margin-top: 50px;
  }
  </style>