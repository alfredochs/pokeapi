<template>
  <div>
    <!-- <button class="btn btn-dark" @click="getAllPokemon">call</button> -->
    <ul class="list-group" v-for="(pokemon, i) in info" :key="i">
      <!-- <li class="list-group-item">{{ pokemon.name }}</li> -->
      <a
        :href="pokemon.url"
        class="list-group-item list-group-item-action"
        aria-current="true"
      >
      {{pokemon.name}}
      </a>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "cardItem",
  data() {
    return {
      info: "",
    };
  },
  methods: {
    getAllPokemon() {
      axios.get("https://pokeapi.co/api/v2/pokemon/").then((resp) => {
        this.info = resp.data.results;
      });
    },
  },
  beforeMount() {
    this.getAllPokemon();
  },
};
</script>
<style>
/* @import "~bootstrap/dist/css/bootstrap.css"; */
</style>