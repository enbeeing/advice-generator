<template>
  <div class="advice-wrapper">
    <Advice :advice="advice" />

    <Separator :mobile="mobile" />

    <DiceButton @advice="displayAdvice" />
  </div>
</template>

<script setup>
import Advice from "./components/Advice.vue";
import Separator from "./components/Separator.vue";
import DiceButton from "./components/DiceButton.vue";
import { ref } from "vue";

const advice = ref(null);
const mobile = window.innerWidth < 380;

const displayAdvice = (value) => {
  advice.value = value;
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Manrope:wght@500&display=swap");

:root {
  --main-font: "Manrope", sans-serif;

  --main-bg-color: hsl(218, 23%, 16%);
  --advice-wrapper-bg-color: hsl(217, 19%, 24%);
  --main-text-color: hsl(193, 38%, 86%);
  --accent-color: hsl(150, 100%, 66%);
  --shadow-color: hsla(218, 23%, 11%);
}

* {
  margin: 0;
  padding: 0;
}

body {
  height: 100vh;
  background: var(--main-bg-color);
  color: var(--main-text-color);
  text-align: center;
  font-family: var(--main-font);
  font-weight: 800;
  font-size: 1rem;
}

#app {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100%;
}

.advice-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background: var(--advice-wrapper-bg-color);
  border-radius: 10px;
  padding: 1rem 1.5rem;
  margin: 0 2rem;
  box-shadow: 0 0 5px var(--shadow-color);
}

p,
svg {
  margin-top: 1.5rem;
}

/* active and hover */
.dice-button:hover,
.dice-button:active {
  box-shadow: 0 0 10px var(--accent-color);
  cursor: pointer;
}

/* desktop */
@media only screen and (min-width: 380px) {
  .advice-wrapper {
    max-width: 450px;
    padding: 1.2rem 2.5rem;
  }
  p {
    margin-top: 30px;
  }
  svg {
    margin-top: 40px;
  }
}
</style>
