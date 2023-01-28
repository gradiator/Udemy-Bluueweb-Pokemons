<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();

const pokeSprite = ref({});

const back = () => {
  router.push("/pokemons"); //Para empujar al usuario a ir a algún sitio, parecido al router link
};

const getData = async () => {
  console.log(route.params.name);
  try {
    const { data } = await axios.get(
      `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
    );
    pokeSprite.value = data.sprites?.front_default;
  } catch (error) {
    console.log(error);
    pokeSprite.value = null;
  }
};

getData();
</script>

<template>
  <main class="text-center">
    <div v-if="pokeSprite">
      <img :src="pokeSprite" alt="" />
      <h1>Pokemon: {{ $route.params.name }}</h1>
    </div>
    <h1 v-else>Pokemon no encontrado...</h1>
    <button @click="back()" class="btn btn-outline-primary">
      Volver al listado
    </button>
  </main>
</template>
