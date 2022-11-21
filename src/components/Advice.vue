<template>
  <div v-if="advice">
    <p class="advice-num">Advice #{{ advice.id }}</p>
    <p class="advice-quote">‘‘{{ advice.advice }}’’</p>
  </div>
  <div v-else>
    <p class="advice-num">Advice</p>
    <p class="advice-quote">{{ loadingSymbol }}</p>
  </div>
</template>

<script setup>
import { onUpdated } from "vue";

const props = defineProps({
  advice: Object,
});

const loadingSymbol = "...";
</script>

<style>
.advice-num {
  color: var(--accent-color);
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  font-weight: normal;
  font-size: small;
}

.advice-quote {
  font-size: 22px;
}
</style>