<script setup lang="ts">
import { onMounted, ref } from "vue";
import listComponent from "@/components/ListComponent.vue";

const itemarray = ref<any>([]);
const itemarray2 = ref<any>([]);

onMounted(() => {
  fetch("https://api.tarkov.dev/graphql", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
    body: JSON.stringify({
      query: `{
items{
name
shortName
avg24hPrice
iconLink
sellFor {
price
source
}
}
}`,
    }),
  })
    .then((r) => r.json())
    .then((data) => {
      data.data.items.forEach((element: any) => {
        if (element.name.includes("N-15")) {
          console.log(element);
        }
        if (element.avg24hPrice != 0) {
          itemarray.value.push(element);
        }
      });
    })
    .then(() => {
      // console.log(itemarray)
      itemarray.value.forEach((element: any) => {
        let highestprice = 0;
        element.sellFor.forEach((buyer: any) => {
          if (buyer.source == "fleaMarket") {
            element.fleaMarketPrice = buyer.price;
          }
        });
        element.sellFor.forEach((buyer: any) => {
          if (buyer.source != "fleaMarket" && buyer.price > highestprice) {
            element.highestBuyer = buyer;
            highestprice = buyer.price;
          }
        });
        if (element.highestBuyer.price > element.fleaMarketPrice) {
          itemarray2.value.push(element);
        }
      });
    })
    .then(() => {
      itemarray2.value.forEach((element: any) => {
        element.profit = element.highestBuyer.price - element.fleaMarketPrice;
      });
    })
    .then(() => {
      itemarray2.value = itemarray2.value.sort((p1: any, p2: any) =>
        p1.profit < p2.profit ? 1 : p1.profit > p2.profit ? -1 : 0
      );
    });
});
</script>

<template>
  <main>
    <listComponent :items="itemarray2" />
  </main>
</template>
