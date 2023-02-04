<script setup lang="ts">
const props = defineProps(["item"]);
</script>

<template>
  <div class="itemcontainer">
    <div class="image_name">
      <img class="icon" :src="props.item.iconLink" :alt="props.item.name" />
      <p>{{ props.item.name }}</p>
    </div>

    <div class="price_container">
       <div class="average_price">
      <p>Average price on market</p>
       <p>{{ props.item.avg24hPrice }}</p>
    </div>
   
    <div class="bestBuyercontainer">
      <p>Best trader</p>
      <p>{{ props.item.highestBuyer.price }}</p>
      <p class="buyer">{{ props.item.highestBuyer.source }}</p>
    </div>
    </div>
   
  </div>
</template>

<style scoped>
p {
  margin: 0;
}
.itemcontainer {
  padding: 1em;
  width: 100%;
  border-top: solid 1px gray;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
}
.image_name{
  display: flex;
  justify-content: space-between;
}
.average_price{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.bestBuyercontainer {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.buyer {
  text-transform: capitalize;
}
.price_container{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.icon {
  width: 64px;
  height: 64px;
}
@media screen and (max-width: 600px) {
  .itemcontainer {
    display: flex;
    flex-direction: column;
  }
}
</style>
