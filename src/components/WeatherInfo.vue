<script setup>
 defineProps(['condition']);
 defineEmits(['remove-place'])
const showMore = defineModel('showMore')
</script>

<template>
    <div class="absolute bg-white/80 backdrop-blur-sm text-slate-900 inset-x-0 bottom-0 rounded-t-lg p-8">
        <!-- Close button -->
        <div class="flex justify-end mb-10">
            <button @click="showMore = false" class="p-1">
                <i class="fa-solid fa-xmark text-xl"></i>
            </button>
        </div>

        <div class="flex items-center justify-between gap-6 mb-20">
            <!-- Wind speed -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-wind mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.wind_kph }} Km/h</p>
                <p>wind</p>
            </div>
            <!-- Humidity level -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-droplet mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.humidity }}</p>
                <p>humidity</p>
            </div>
            <!-- Precipitation -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-umbrella mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.precip_in }}</p>
                <p>precipitation</p>
            </div>
        </div>
        <div class="flex items-center justify-between gap-6 mb-10">
            <!-- Wind direction -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-fan mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.wind_dir }}</p>
                <p>direction</p>
            </div>
            <!-- Feels like -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-temperature-half mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.feelslike_c }}&deg;</p>
                <p>Feels</p>
            </div>
            <!-- UV -->
            <div class="text-center flex-1">
                <i class="fa-solid fa-sun mb text-2xl"></i>
                <p class="text-xl font-bold">{{ condition.uv }}</p>
                <p>UV index</p>
            </div>
        </div>
        <!-- Last update and delete -->
        <div class="flex justify-between items-center">
            <h3 class="text-slate-900/50">last update: {{ condition.last_updated }}</h3>
            <button @click="$emit('remove-place')">
                <i class="fa-solid fa-trash"></i>
            </button>
        </div>
    </div>
</template>