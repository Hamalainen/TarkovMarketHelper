<script setup lang="ts">
const props = defineProps(["item"]);
</script>

<template>
  <div class="itemcontainer">
    <img class="icon" :src="props.item.iconLink" :alt="props.item.name" />
    <p>{{ props.item.name }}</p>
    <p>{{ props.item.avg24hPrice }}</p>
    <div class="bestBuyercontainer">
      <p>{{ props.item.highestBuyer.price }}</p>
      <p class="buyer">{{ props.item.highestBuyer.source }}</p>
    </div>
  </div>
</template>

<style>
p{
    margin: 0;
}
.itemcontainer {
    padding: 1em;
  width: 50vw;
  border-top: solid 1px gray;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  gap: 3rem;
}
.bestBuyercontainer {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.buyer{
    text-transform: capitalize;
}

</style>
