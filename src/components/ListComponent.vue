<script setup lang="ts">
import ItemComponent from "./ItemComponent.vue";
const props = defineProps(["items"]);
</script>

<template>
  <div class="main">

      <div class="header_list">
        <p class="iconplaceholder"></p>
        <p>Name</p>
        <p>Average prive on market</p>
        <p>Best trader</p>
      </div>
      <ItemComponent
        v-for="(item, index) in props.items"
        v-bind:key="index"
        :item="item"
      />
    </div>

</template>
<style>
.header_list {
  padding: 1em;
  gap: 3rem;
  width: 50vw;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
}
.iconplaceholder {
  width: 64px;
}
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem;
}

</style>
