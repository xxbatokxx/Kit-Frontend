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
      "https://zullkit-backend.belajarkoding.com/api/products?id="
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
    <div class="container px-4 mx-auto my-16 md:px-12" id="products">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <ItemsCard
            v-for="item in items"
            :id="item.id"
            :key="item.id"
            :title="item.name"
            :desc="item.subtitle"
            :image="item.thumbnails"
            />
        </div>
    </div>
</template>