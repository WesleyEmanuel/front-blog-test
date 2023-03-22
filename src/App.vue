<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
  <header></header>

  <RouterView />
</template>

<style>
body {
  background-color: #24232b;
}
body::-webkit-scrollbar {
  width: 15px; /* width of the entire scrollbar */
}

body::-webkit-scrollbar-track {
  background: #24232b;
}

body::-webkit-scrollbar-thumb {
  background-color: rgb(134, 79, 236);
  border-radius: 20px;
  border: 3px solid #24232b;
}
</style>
