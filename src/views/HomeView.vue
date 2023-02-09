<script setup>
import { useCounterStore } from "@/store/counter.js";
import { storeToRefs } from "pinia";

const useCounter = useCounterStore();
</script>
<template>
  <main>
    <h1>Home counter: {{ useCounter.count }}</h1>
    <h2>Double: {{ useCounter.double }}</h2>
    <button @click="useCounter.increment">Increment</button>
  </main>
</template>
