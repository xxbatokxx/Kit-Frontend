<script setup>

import { ref } from 'vue'

const props = defineProps({
    defaultImage: String,
    galleries: Array
})

const thumbnails = ref(props.defaultImage)

function changeImage(Image) {
    this.thumbnails= Image
}

</script>

<template>
    <section id="gallery">
        <img :src="thumbnails" alt="" class="w-full mt-6 rounded-2xl">
        <div class="grid grid-cols-4 gap-4 mt-4">
            <template v-for="gallery in galleries" :key="gallery.id">
                <div @click="changeImage(gallery.url)"
                    class="overflow-hidden cursor-pointer rounded-2xl"
                    :class="{ 'ring-2 ring-indigo-500': thumbnails == gallery.url }">
                    <img :src="gallery.url" class="w-full" alt="">
                </div>
            </template>
        </div>
    </section>
</template>