<script lang="ts" setup>
import { store } from '@src/store/store'

import MainProfile from '@src/components/home/MainProfile.vue'

import { socketEmitter } from '@src/components/utils/UtilsTools.vue'
import { onEnterPress } from '@src/components/utils/KeyPress.vue'

store.layout.footer.next.callback = async () => {
    await store.profiles.save()
    store.profiles.newProfileId = 0
    socketEmitter(store.socket, 'disconnectObs')

    store.redirect.path = '/home'
}

onEnterPress(() => {
    if (store.layout.footer.next.trigger) {
        store.layout.footer.next.trigger()
    }
})


</script>

<template>
    <div class="flex flex-col w-full pb-10">
        <div class="flex items-center bg-bg-2 text-content-2 text-sm p-4">
            <span class="emoji">✌️</span>
            <p>Check if everything looks good !</p>
        </div>
        <MainProfile />
    </div>
</template>