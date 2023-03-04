<script setup>
import {ref} from "vue";

let adviceId = ref("");
let adviceQuote = ref("");
let showLoader = ref(false);

const getAdvice = async () => {
    showLoader.value = !showLoader.value;
    
    const url = "https://api.adviceslip.com/advice";
    const data = await sendFetchRequest(url);
    
    setTimeout(() => {
        setAdvice(data);
        showLoader.value = !showLoader.value;
    }, 500);

}

const sendFetchRequest = async (url) => {
    let response = await fetch(url);
    if (response.ok) {
        response = await response.json();
        return response;
    } else {
        alert("Error HTTP: " + response.status);
    }
}

const setAdvice = (data) => {
    adviceId.value = data.slip.id;
    adviceQuote.value = data.slip.advice;
}


getAdvice();

</script>
<template>
    <div class="advice">
        <div class="advice__loader" v-if="showLoader"></div>
        <div class="advice__content" v-else>
            <h1 class="advice__title">Advice #{{ adviceId }}</h1>
            <p class="advice__quote">“{{ adviceQuote }}”</p>
            <div class="advice__hr"></div>
            <button class="advice__generator" @click="getAdvice"><img class="advice__generator-img" src="/src/assets/images/icon-dice.svg" alt=""></button>
        </div>
    </div>
</template>

<style scoped>
.advice {
    max-width: 400px;
    min-height: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 1rem;
    padding: 2rem 1.5rem 3rem;
    background: var(--blue-800);
    border-radius: 10px;
}
@media (min-width: 450px) {
    .advice {
        min-width: 300px;
        min-height: 200px;
    }
}
.advice__content {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}
.advice__title {
    margin: 0 0 1.25rem;
    text-transform: uppercase;
    font-size: 10px;
    font-weight: var(--fw-extra-bold);
    color: var(--green-100);
    letter-spacing: 3px;
}
.advice__quote {
    /* font-size: var(--fs-base); */
    margin: 0 0 1rem;
    font-size: var(--fs-base);
    font-weight: var(--fw-extra-bold);
    text-align: center;
}
.advice__hr {
    height: 30px;
    width: 100%;
    background: url(/src/assets/images/pattern-divider-mobile.svg) no-repeat center;
}
@media (min-width: 450px) {
    .advice__hr {
        background: url(/src/assets/images/pattern-divider-desktop.svg) no-repeat center/90%;
    }
}
.advice__generator {
    width: 50px;
    height: 50px;
    background: var(--green-100);
    border: none;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    position: absolute;
    top: 125%;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.advice__generator:hover {
    box-shadow: 0 0 2rem 0 var(--green-100);
}
.advice__generator-img {
    width: 20px;
    height: 20px;
}
.advice__loader {
  display: inline-block;
  width: 45px;
  height: 45px;
}
.advice__loader:after {
  content: " ";
  display: block;
  width: 45px;
  height: 45px;
  border-radius: 50%;
  border: 6px solid var(--green-100);
  border-color: var(--green-100) transparent var(--green-100) transparent;
  animation: load 1.7s linear infinite;
}
@keyframes load {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>