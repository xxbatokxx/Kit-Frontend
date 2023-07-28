<script setup>
import { ref, onMounted } from 'vue';
import axios from  'axios'
import ItemsCard from '../ItemsCard.vue';

// put data api in here
const items = ref([])

async function getItems() {
  try {
    // get data
    const response = await axios.get(
      "https://zullkit-backend.belajarkoding.com/api/products"
    );
    // handle data success
    console.log(response.data);
    items.value = response.data.data.data;
  } catch (err) {
    // handle data errorr
    console.error(err);
  }
}

// a process data if get data success
onMounted(() => {
    getItems()
})

</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <ItemsCard
            v-for="Itemscard in items"
            :key="Itemscard.id"
            :id="ItemsCard.id"
            :title="Itemscard.name"
            :desc="Itemscard.subtitle"
            :image="Itemscard.thumbnails"
            />
        </div>
    </div>
</template>