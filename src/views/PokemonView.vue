<script setup>
import { useRoute, useRouter } from "vue-router";
import { useGetData } from "@/composable/getData.js";

const route = useRoute();
const router = useRouter();

const { data, getData, loading, errorData } = useGetData();
const back = () => {
  router.push("/pokemons"); //Para empujar al usuario a ir a algún sitio, parecido al router link
};

getData(`https://pokeapi.co/api/v2/pokemon/${route.params.name}`);
</script>

<template>
  <p v-if="loading">Cargando información...</p>
  <div class="alert alert-danger mt-2" v-if="errorData">{{ errorData }}</div>
  <div v-if="data">
    <img :src="data.sprites?.front_default" alt="" />
    <h1>Pokemon: {{ $route.params.name }}</h1>
  </div>
  <button @click="back()" class="btn btn-outline-primary">
    Volver al listado
  </button>
</template>
