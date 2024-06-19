<script setup>
import { computed, ref } from "vue";
import SearchField from './components/SearchField.vue';
import WeatherCard from './components/WeatherCard.vue';
let date = computed(() => new Date().toLocaleDateString('en-us', {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric'
}))

let places = ref([]);
const addPlace = (place) => {
    places.value.push(place)
}

const deletePlace = (name) => {
    console.log(name);
    places.value = places.value.filter(item => item.location.name !== name)
}
</script>

<template>
    <div class="container mx-auto flex flex-col items-center justify-center">
        <div>
            <p class="text-3xl">{{ date }}</p>
        </div>
        <SearchField @place-list="addPlace" />
    </div>
    <div class="flex gap-x-4 flex-wrap items-center justify-center">
        <WeatherCard @delete-place="deletePlace" :place="place" :key="place.location.name" v-for="place in places" />
    </div>
</template>

<style scoped></style>
