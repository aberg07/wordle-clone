<script setup lang="ts">
let secretWord = 'RANGE'
let modalMessage = '';
let userInput = ref<String[]>(['', '', '', '', '', '']);
let colorArray = ref<String[][]>([]); //<String[][]> tells TS that we intend to store arrays of strings in this array so it doesn't infer that this array will always be empty
let currentIndex = ref(0);
let numTries = 0;
let showModal = ref(false);
let answerArray = ref<String[]>(['', '', '', '', '', '']);
let currentInput = computed(() => {
    return userInput.value[currentIndex.value];
})

onMounted(() => {
    document.addEventListener("keydown", handleKey)
})
onUnmounted(() => {
    document.removeEventListener("keydown", handleKey);
})
function handleKey(e: KeyboardEvent) {
    //Delete letters when user hits backspace
    if (e.key === "Backspace") userInput.value[currentIndex.value] = userInput.value[currentIndex.value].slice(0, userInput.value[currentIndex.value].length-1);
    //Else if user types a single letter, accept it as valid input
    else if (currentInput.value.length+1 <= 5 && /^[a-z]{1}$/i.test(e.key)) {
        userInput.value[currentIndex.value] += e.key.toUpperCase();
    }
    else if (e.key === "Enter") {
        checkAnswer();
    }
}

//TODO: Write checkAnswer function and get props to work with WordRow to indicate correct, "off", or incorrect letters
function checkAnswer() {
    let colors = [];
    for (let i = 0; i < userInput.value.length; i++) {
        if (userInput.value[currentIndex.value][i] === secretWord[i]) {
            colors.push('right');
        }
        else if (secretWord.indexOf(userInput.value[currentIndex.value][i]) !== -1) {
            colors.push('off')
        }
        else colors.push('wrong');
    }
    colorArray.value.push(colors);
    numTries++;
    if (userInput.value[currentIndex.value] == secretWord) {
        modalMessage = 'Well done!'
        showModal.value = true;
    }
    else if (numTries >= 6) {
        modalMessage = 'Oh no!'
        showModal.value = true;
    }
    currentIndex.value++;
}

function reset() {
    numTries = 0;
    currentIndex.value = 0;
    userInput.value = ['', '', '', '', '', ''];
    colorArray.value = [];
    showModal.value = false;
}
</script>

<template>
    <h1 class="text-4xl pt-4 pb-8 text-center text-white">Wordle Clone</h1>
    <div class="flex flex-col gap-y-2 h-80v">
        <WordRow v-for="(answer, i) in answerArray" v-model:input="userInput[i]" :answerArray="colorArray[i]"/>
    </div>
    <Modal v-if="showModal" @reset="reset()">
        <template #body>
            <p>{{ modalMessage }}</p>
        </template>
    </Modal>
    <footer class="h-5v border-t-2 border-gray-700 mt-4 text-red-700">
        <p class="text-center text-sm px-20">This website is made only for educational purposes. Wordle is property of The New York Times. I do not own or claim to own it in any way.</p>
    </footer>
</template>

<style scoped>
</style>