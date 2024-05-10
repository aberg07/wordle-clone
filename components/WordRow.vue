<script setup lang="ts">
const props = defineProps({
    input: String,
    answerArray: {
        type: Array<String>,
    }
});
</script>

<template>
    <div class="flex flex-row justify-center items-center gap-x-1">
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="`bg-${answerArray?.at(0)}-400`">{{ props.input?.substring(0,1) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="`bg-${answerArray?.at(1)}-400`">{{ props.input?.substring(1,2) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="`bg-${answerArray?.at(2)}-400`">{{ props.input?.substring(2,3) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="`bg-${answerArray?.at(3)}-400`">{{ props.input?.substring(3,4) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="`bg-${answerArray?.at(4)}-400`">{{ props.input?.substring(4,5) }}</div>
    </div>
</template>