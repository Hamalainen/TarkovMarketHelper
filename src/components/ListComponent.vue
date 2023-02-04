<script setup lang="ts">
import { ref } from "vue";
import ItemComponent from "./ItemComponent.vue";
import ItemComponentMobile from "./ItemComponentMobile.vue";
const props = defineProps(["items"]);
const innerwidth = ref(0);
innerwidth.value = window.innerWidth;
addEventListener("resize", (event) => {
  innerwidth.value = window.innerWidth;
});
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
      v-if="innerwidth > 600"
      v-for="(item, index) in props.items"
      v-bind:key="index"
      :item="item"
    />
    <ItemComponentMobile
      v-else
      v-for="(item, index) in props.items"
      v-bind:key="index + '_mobile'"
      :item="item"
    />
  </div>
</template>
<style scoped>
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
@media screen and (max-width: 600px) {
  .header_list {
    display: none;
  }
}
</style>
