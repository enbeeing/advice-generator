<template>
  <div class="dice-button" @click="rollNewAdvice">
    <img
      src="../assets/icon-dice.svg"
      alt="dice img, click and roll for new advice"
    />
  </div>
</template>

<script setup>
const emit = defineEmits(["advice"]);

const rollNewAdvice = async () => {
  await fetch("https://api.adviceslip.com/advice", { cache: "no-cache" })
    .then((res) => res.json())
    .then((data) => {
      emit("advice", data.slip);
    })
    .catch((err) => console.log(err.message));
};
</script>

<style>
.dice-button {
  background: var(--accent-color);
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 1.2rem;
  border-radius: 50%;
  transform: translateY(50%);
  transition: 0.2s;
}

/* active and hover */
.dice-button:hover,
.dice-button:active {
  box-shadow: 0 0 10px var(--accent-color);
  cursor: pointer;
}
</style>