<script lang="ts" setup>
import { useRouter } from 'vue-router'

import Gabin from '@src/components/basics/GabinFace.vue'
import ArrowRightIcon from '@src/components/icons/ArrowRightIcon.vue'
import ButtonUi from '@src/components/basics/ButtonUi.vue'
import { onEnterPress } from '@src/components/utils/KeyPress.vue'

const router = useRouter()

const goNext = (route: string) => {
    router.push('/setup/'+route)
}

onEnterPress(() => {
    goNext('obs')
})

</script>

<template>
    <div class="h-full w-full flex justify-center items-center">
        <div class="w-96 flex flex-col justify-start items-start">
            <Gabin
                msg="My video mixer?"
                size="sm"
            />

            <h1 class="my-4">
                Choose your video mixer
            </h1>
            <span class="text-content-2 text-sm">
                Please let Gabin know what mixer you'll use on this profile.
            </span>

            <div class="w-full flex flex-col justify-start items-center">
                <ButtonUi
                    class="w-full my-2"
                    @click="goNext('obs')"
                >
                    OBS <ArrowRightIcon />
                </ButtonUi>
                <ButtonUi
                    class="w-full my-2"
                    :disabled="true"
                    @click="goNext('obs')"
                >
                    ATEM <ArrowRightIcon />
                </ButtonUi>
                <ButtonUi
                    class="w-full my-2"
                    :disabled="true"
                    @click="goNext('obs')"
                >
                    Other <ArrowRightIcon />
                </ButtonUi>
            </div>

            <!-- <div class="mt-5 w-full flex justify-between">
                <ButtonUi
                    class="w-full "
                    @click="goBack"
                >
                    <ArrowLeftIcon />
                    Back
                </ButtonUi>
            </div> -->
        </div>
    </div>
</template>