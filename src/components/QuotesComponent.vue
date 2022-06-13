<template>
  <div class="min-h-screen flex flex-column justify-content-center align-items-center">
    <h1 class="text-center">Good quote for good vibes</h1>
    <div :id="quotetype.id" class="m-3"><p>{{ quotetype.content }}</p>
      <span class="author-name">- {{ quotetype.originator.name }}</span></div>
    <Button :label="buttonState.label" :icon='buttonState.icon' iconPos="right" @click="getQuote"
            :disabled="buttonState.label === loadingState.label"/>
  </div>
</template>


<script setup>
import Button from 'primevue/button';
import {ref, onMounted} from 'vue';

const axios = require("axios");

let quotetype = ref({
  id: 1230292,
  language_code: "en",
  content: "There's good in all of us and I think I simply love people too much, so much that it makes me feel too sad.",
  url: "https://quotepark.com/quotes/1230292-kurt-cobain-theres-good-in-all-of-us-and-i-think-i-simply-lov/",
  originator: {
    id: 130635,
    name: "Kurt Cobain",
    url: "https://quotepark.com/authors/kurt-cobain/"
  },
  tags: [
    "Feeling",
    "People",
    "Sadness",
    "Love",
    "Thinking",
    "feel",
    "good",
    "goodness",
    "making",
    "use"
  ]
});

let initalState = {
  label: 'Get new Quote',
  icon: ''
};
let loadingState = {
  label: 'Getting...',
  icon: 'pi pi-spin pi-spinner'
};
let afterGetting = {
  label: 'Got the new quote',
  icon: 'pi pi-check'
};

let buttonState = ref({
  label: '',
  icon: ''
});

let options = {
  method: 'GET',
  params: {language_code: 'en'},
  headers: {
    'X-RapidAPI-Key': 'd76feacf84mshd9d8fc82bf32673p157495jsnc9cd75019eb9',
    'X-RapidAPI-Host': 'quotes15.p.rapidapi.com'
  }
};

onMounted(() => {
  buttonState.value = initalState;
  getQuote();
});

function getQuote() {
  buttonState.value = loadingState;
  setTimeout(function () {
    //your code to be executed after 1 second
    axios.request("https://quotes15.p.rapidapi.com/quotes/random/", options).then(function (response) {
      buttonState.value = afterGetting;
      quotetype.value = response.data;
    }).catch(function (error) {
      console.error(error);
    });
  }, 3000);
  setTimeout(function () {
    buttonState.value = initalState;
  }, 5000);
}
</script>

<style scoped>
.author-name{
  float: right;
}
</style>