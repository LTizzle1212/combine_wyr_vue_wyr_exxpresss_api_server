<script setup>
import { ref } from 'vue'

defineProps({
  question: String,
  answer1: String,
  answer2: String
})

const emit = defineEmits( [
  'answer-selected'
])

const choice = ref(null)  // null means no value 
// needed to prevent both buttons being selected 
// when the page first loads since if the two answer1 and answer2 values are the same 
// as the initial value for choice, Vue will select both radio buttons

function choiceMade() {
  emit('answer-selected', choice.value)
}

</script>

<template>

<div id="wyr">

  <h2>Make your choice!</h2>

  <div id="question">
    {{ question }}
  </div>

  <div id="answers">
    <input type="radio" id="answer-1" v-model="choice" v-bind:value="answer1" v-on:change="choiceMade">
    <label for="answer-1"> {{ answer1 }}</label>

    <input type="radio" id="answer-2" v-model="choice" v-bind:value="answer2" v-on:change="choiceMade">
    <label for="answer-2"> {{ answer2 }}</label>
  </div>

</div>
</template>

<style scoped>

#wyr {
  background-color: hotpink;
  padding: 20px;
}

#answers {
  padding: 10px;
}

</style>