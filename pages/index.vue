<script setup lang="ts">
let secretWord = 'RANGE'
let userInput = ref('');
let answerArray = ref<String[]>([]); //<String[]> tells TS that we intend to store strings in this array so it doesn't infer that this array will always be empty

onMounted(() => {
    document.addEventListener("keydown", handleKey)
})
onUnmounted(() => {
    document.removeEventListener("keydown", handleKey);
})
function handleKey(e: KeyboardEvent) {
    //Delete letters when user hits backspace
    if (e.key === "Backspace") userInput.value = userInput.value.slice(0, userInput.value.length-1);
    //Else if user types a single letter, accept it as valid input
    else if (userInput.value.length+1 <= 5 && /^[a-z]{1}$/i.test(e.key)) {
        userInput.value += e.key.toUpperCase();
    }
    else if (e.key === "Enter") checkAnswer();
}

//TODO: Write checkAnswer function and get props to work with WordRow to indicate correct, "off", or incorrect letters
function checkAnswer() {
    answerArray.value = [];
    for (let i = 0; i < userInput.value.length; i++) {
        if (userInput.value[i] === secretWord[i]) {
            answerArray.value.push('green');
        }
        else if (secretWord.indexOf(userInput.value[i]) !== -1) {
            answerArray.value.push('yellow')
        }
        else answerArray.value.push('red');
    }
    console.log(answerArray.value);
}
</script>

<template>
    <h1 class="text-2xl text-center">Wordle Clone</h1>
    <div class="flex flex-col gap-y-2">
        <WordRow v-model:input="userInput" :answerArray="answerArray"/>
        <WordRow />
        <WordRow />
        <WordRow />
        <WordRow />
        <WordRow />
    </div>
</template>