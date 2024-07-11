<script setup lang="ts">

</script>

<template>
    <div class='modal-backdrop flex justify-center place-items-center bg-[#0000004D] fixed top-0 bottom-0 left-0 right-0'>
        <div class='modal flex flex-col shadow-2xl bg-[#FFFFFF] overflow-x-auto w-1/4 h-1/3'>
            <div class="flex flex-col gap-y-8 justify-center place-items-center h-full">
                <slot name="body">
                </slot>
                <button type="button" class="border-2 w-52" @click="$emit('reset')">
                    Play again?
                </button>
            </div>
        </div>
    </div>
</template>