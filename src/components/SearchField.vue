<script setup>
import { reactive } from 'vue'
import axios from 'axios'

const emit = defineEmits(['place-list'])

let searchTerm = reactive({
    query: '',
    timer: null,
    result: null
})

const searchHandler = () => {
    clearTimeout(searchTerm.timer);
    searchTerm.timer = setTimeout(async () => {
        if (searchTerm.query !== '') {
            let result = await axios.get(`http://api.weatherapi.com/v1/search.json?key=f237d30c4e5e4f36b3b164240241806&q=${searchTerm.query}`);
            searchTerm.result = result.data;
        } else {
            searchTerm.result = null
        }
    }, 500);
}

const getWeather = async (name) => {
    console.log(name);
    let result = await axios.get(`http://api.weatherapi.com/v1/forecast.json?key=f237d30c4e5e4f36b3b164240241806&q=${name}&days=3&aqi=no&alerts=no`);
    emit('place-list', result.data);
    searchTerm.query = ''
    searchTerm.result = null
}

</script>

<template>
    <div class="mt-10 w-1/2">
        <!-- search field -->
        <form>
            <div class="bg-white border border-indigo-600/30 rounded-lg shadow-lg flex items-center">
                <i class="fa-solid fa-magnifying-glass p-2 text-indigo-600"></i>
                <input type="text" placeholder="Search for a place"
                    class="rounded-r-lg p-2 border-0 outline-0 focus:ring-2 focus:ring-indigo-600 ring-inset w-full"
                    v-model.trim="searchTerm.query" @input="searchHandler" />
            </div>
        </form>
        <!-- search suggestions -->
        <div class="bg-white my-2 rounded-lg shadow-lg max-h-[200px] overflow-y-scroll">
            <div v-if="searchTerm.result">
                <button :key="place.id" @click="getWeather(place.name)"
                    class="px-3 my-2 hover:text-indigo-600 hover:font-bold w-full text-left"
                    v-for="place in searchTerm.result">{{ place.name }}, {{ place.region }}, {{ place.country
                    }}</button>
            </div>
        </div>
    </div>
</template>