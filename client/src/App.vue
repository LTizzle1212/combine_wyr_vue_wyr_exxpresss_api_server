<script setup>

import { ref, onMounted } from 'vue'
import wyrService from './services/wyrService'

import WouldYouRather from './components/WouldYouRather.vue'


// Data for the question, and two answers
const wyrQuestion = ref('')
const wyrAnswer1 = ref('')
const wyrAnswer2 = ref('')

// Will store the user's selection, either 'Triangle house' or 'Circle house'
const userSelection = ref('')


onMounted( () => {
  wyrService.getRandomWYR().then( (wyrData) => {
    // Expect wyrData to be something like 
    // {"question":"Play any musical instrument or speak any language?","answer1":"Play any musical instrument","answer2":"Speak any language"}
    // "answer1": "Play any musical instrument",
    // "answer2": "Speak any language"

    wyrQuestion.value = wyrData.question 
    wyrAnswer1.value = wyrData.wyrAnswer1
    wyrAnswer2.value = wyrData.wyrAnswer2
  })
})

function updateUserSelection(userChoice) {
  userSelection.value = `Thanks! You chose ${userChoice}`
}

</script>

<template>

<div id="app">
  <h1>Hello! Would You Rather...</h1>

  <WouldYouRather>
    v-bind:question="wyrQuestion"
    v-bind:answer1="wyrAnswer1"
    v-bind:answer2="wyrAnswer2"
    v-on:answer-selected="updateUserSelection"
  </WouldYouRather>

   {{ userSelection }} 
  
</div>

</template>

<style scoped>

#app {
  background-color: aqua;
}

</style>
