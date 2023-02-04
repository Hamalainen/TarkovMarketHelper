<script setup lang="ts">
import { onMounted, ref } from 'vue';
import listComponent from '@/components/ListComponent.vue'

  const itemarray = ref<any>([]);
  const itemarray2 = ref<any>([]);

  


onMounted(() => {
  fetch('https://api.tarkov.dev/graphql', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Accept': 'application/json',
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
}`})
})
    .then(r => r.json())
    .then(data => {
        data.data.items.forEach((element:any) => {
            if (element.avg24hPrice != 0) {
                itemarray.value.push(element);
            }
        });
    }).then(() => {
        itemarray.value.forEach((element:any) => {
            let highestprice = 0;
            element.sellFor.forEach((buyer:any) => {
                if (buyer.source != 'fleaMarket' && buyer.price > highestprice) {
                    element.highestBuyer = buyer;
                    highestprice = buyer.price;
                }
            })
            if (element.highestBuyer.price > 15000 && element.highestBuyer.price > element.avg24hPrice-2000) {
                itemarray2.value.push(element);
            }

        })
        console.log(itemarray2);
    })
})







</script>

<template>
  <main>
    <listComponent :items="itemarray2"/>
  </main>
</template>

