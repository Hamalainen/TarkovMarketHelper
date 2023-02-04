<script setup lang="ts">
import {  RouterView } from 'vue-router'
import HeaderComponent from './components/HeaderComponent.vue';
</script>

<template>
  <div class="background">
    <div class="background_smear">
      <HeaderComponent/>
      <RouterView />
    </div>
  </div>
</template>
<style>
*{
  color: white;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
.background {
  overflow: auto;
  height: 100vh;
  width: 100vw;
  background-image: url(@/assets/backgroundTarkov.webp);
  background-position: center;
  position: fixed;
}
.background_smear{
  background-color: rgba(0, 0, 0, 0.8);
  width: 100%;
}
</style>