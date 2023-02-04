<script setup lang="ts">
import {  RouterView } from 'vue-router'
import HeaderComponent from './components/HeaderComponent.vue';
</script>

<template>
  <HeaderComponent/>
  <div class="background">
    <div class="background_smear">
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
  height: calc(100vh - 6vh);
  width: 100vw;
  background-image: url(@/assets/backgroundTarkov.webp);
  background-repeat: repeat-y;
  background-position: center;
  background-size: 100vw 100vh;
  position: fixed;
}
.background_smear{
  background-color: rgba(0, 0, 0, 0.8);
}
</style>