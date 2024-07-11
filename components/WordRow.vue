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
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="answerArray?.at(0)">{{ props.input?.substring(0,1) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="answerArray?.at(1)">{{ props.input?.substring(1,2) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="answerArray?.at(2)">{{ props.input?.substring(2,3) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="answerArray?.at(3)">{{ props.input?.substring(3,4) }}</div>
        <div class="flex items-center justify-center border-2 border-black w-16 h-16 text-2xl" :class="answerArray?.at(4)">{{ props.input?.substring(4,5) }}</div>
    </div>
</template>

<style scoped>
.off {
    background-color: yellow;
}
.wrong {
    background-color: red;
}
.right {
    background-color: green;
}
</style>