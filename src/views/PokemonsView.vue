<script setup>
import { RouterLink } from "vue-router";
import { useGetData } from "@/composable/getData.js";

const { data, getData, loading, errorData } = useGetData();

getData("https://pokeapi.co/api/v2/pokemon");
</script>

<template>
  <h1>Pokemons</h1>
  <p v-if="loading">Cargando información...</p>
  <div class="alert alert-danger mt-2" v-if="errorData">{{ errorData }}</div>
  <div v-if="data">
    <ul class="list-group">
      <li
        class="list-group-item"
        v-for="pokemon in data.results"
        :key="pokemon.id"
      >
        <router-link :to="`/pokemons/${pokemon.name}`">{{
          pokemon.name
        }}</router-link>
      </li>
    </ul>
    <div class="mt-2">
      <button
        :disabled="!data.previous"
        class="btn btn-warning me-2"
        @click="getData(data.previous)"
      >
        Anterior
      </button>

      <button
        :disabled="!data.next"
        class="btn btn-primary"
        @click="getData(data.next)"
      >
        Posterior
      </button>
    </div>
  </div>
</template>
