<script setup>
import { onBeforeMount } from 'vue'
const props = defineProps(['forecast'])

</script>

<template>
    <div class="mb-2 flex items-center justify-between">
        <table class="w-full">
            <tr>
                <!-- day of the week -->
                <td class="w-1/3">{{ props.forecast.date }}</td>

                <!-- icon -->
                <td class="w-1/3">
                    <img :src="props.forecast.day.condition.icon" alt="icon" width="30" class="mx-auto" />
                </td>

                <!-- high/low temp -->
                <td class="w-1/3 text-right">{{ props.forecast.day.maxtemp_c }}/{{ props.forecast.day.mintemp_c }}</td>
            </tr>
        </table>
    </div>
</template>