<script setup>
import { ref, reactive } from 'vue';
import New from './components/new.vue';
import TheWelcome from './components/TheWelcome.vue';
</script>

<template>
  <header>
    <img src="./assets/img/logoW.png" alt="logo" id="logo1">
    <h1>Bienvenue sur Wallet Wizard !</h1>
 </header>

  <main>
    <New />
  </main>
</template>

<style scoped>
</style>
