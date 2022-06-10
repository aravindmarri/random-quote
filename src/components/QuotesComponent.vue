<template>
  <h1>Hello</h1>
  <Button label="Get new!" icon="pi pi-check" iconPos="right"  @click="getQuote"/>
  <p>{{quote}}</p>
</template>


<script setup>
import Button from 'primevue/button';
import { ref } from 'vue'
import {onMounted} from "vue";
const axios = require("axios");
let quote  = ref()

let options = {
  method: 'GET',
  params: {language_code: 'en'},
  headers: {
    'X-RapidAPI-Key': 'd76feacf84mshd9d8fc82bf32673p157495jsnc9cd75019eb9',
    'X-RapidAPI-Host': 'quotes15.p.rapidapi.com'
  }
};

onMounted(() => {
  getQuote();
});

function getQuote(){
  axios.request("https://quotes15.p.rapidapi.com/quotes/random/", options).then(function (response) {
    console.log(response.data);
    quote = response.data;
  }).catch(function (error) {
    console.error(error);
  });
}

</script>

<style scoped>

</style>