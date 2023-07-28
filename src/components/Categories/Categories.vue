<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";

import CategoriesCard from "./../CategoriesCard.vue";

// put data api in here
const categories = ref([]);

async function getCategories() {
    try {
        // get data
        const response = await axios.get(
            "https://zullkit-backend.belajarkoding.com/api/categories"
        );
        // handle data success
        console.log(response.data);
        categories.value = response.data.data.data;
    } catch (err) {
        // handle data errorr
        console.error(err);
    }
}

// a process data if get data success
onMounted(() => {
    getCategories();
});
</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12" id="categories">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">All Categories</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">
            <CategoriesCard v-for="category in categories" :id="category.id" :key="category.id" :title="category.name"
                :count="0" :image="category.thumbnails" />
        </div>
    </div>
</template>
