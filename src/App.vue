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
  padding: 1.2rem 1rem 0 1rem;
  margin: 0 2rem;
  box-shadow: 0 0 5px var(--shadow-color);
}
</style>
