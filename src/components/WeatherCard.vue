<script setup>
import { onBeforeMount, ref } from 'vue'
import BorderLine from './BorderLine.vue'
import WeatherInfo from './WeatherInfo.vue'
import WeatherForCast from './WeatherForCast.vue'
const props = defineProps(['place']);
const { place } = props
const isDay = ref(place.current.is_day)
let showMore = ref(false)
onBeforeMount(() => {
    console.log(props.place);
})
</script>

<template>
    <div class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden" :class="[isDay?'bg-blue-500':'bg-slate-700']">
        <!-- Location & time -->
        <div class="mb-2 flex justify-between items-center">
            <div class="flex items-center justify-center gap-2">
                <i class="fa-solid fa-location-dot"></i>
                <h1 class="text-3xl">{{ place.location.name }}</h1>
            </div>
            <div class="flex items-center justify-center gap-2">
                <i class="fa-solid fa-clock"></i>
                <h1 class="text-3xl">{{ new Date(place.location.localtime).toLocaleTimeString() }} </h1>
            </div>
        </div>

        <!-- current weather -->
        <div class="text-center flex-1">
            <img :src="place.current.condition.icon" alt="icon" width="200" class="mx-auto -mb-10" />
            <h1 class="text-9xl mb-2">{{ place.current.temp_c }}&deg;</h1>
            <p class="text-2xl">{{ place.current.condition.text }}</p>
        </div>

        <BorderLine />

        <!-- forecast -->
        <div>
            <WeatherForCast :forecast="forecast" :key="ind" v-for="(forecast,ind) in place.forecast.forecastday " />
        </div>

        <!-- info -->
        <div v-show="showMore">
            <WeatherInfo @remove-place="$emit('delete-place', place.location.name)" v-model:showMore="showMore"
                :condition="place.current" />
        </div>

        <!-- forecast btn -->
        <div class="flex justify-end items-center gap-1 mt-10">
            <button @click="showMore = true">More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i></button>
        </div>
    </div>
</template>