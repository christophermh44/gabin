<script lang="ts" setup>

import { useRouter } from 'vue-router'
import { store } from '@src/store/store'

import loading from '@src/assets/pictures/loading.gif'
import { fetchProfiles } from '@src/components//setup/FetchProfile.vue';

const router = useRouter()

fetchProfiles(() => {
    const route = store.redirect.path? store.redirect.path : '/home'
    router.push(route)
})


</script>


<template>
    <div class="h-full w-full flex justify-center items-center">
        <div class="h-80 flex flex-col justify-start items-center">
            <div
                class="w-40 h-40 min-h-40 rounded-full overflow-hidden bg-no-repeat bg-center"
                :style="{ backgroundImage: `url(${loading})`, backgroundSize: '225px' }"
            />
            <h2 class="mt-16 mb-4">
                Preparing your Gabin
            </h2>
            <span class="text-content-2 text-sm">Wait a few second Gabin is cooking some cookies</span>
        </div>
    </div>
</template>