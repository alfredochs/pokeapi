<template>
  <div>
    <button class="btn btn-danger" @click="customPokemonData">Add</button>
    <div class="row">
      <div class="col-6" v-for="(pokemon, i) in customInfo" :key="i">
        <div class="card h-100">
          <div class="card-body">
            <img :src="pokemon.img" class="card-img-top" alt="...">
            <h5 class="card-title">{{ pokemon.name }}</h5>
            <a :href="pokemon.url" class="btn btn-primary">More Data</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "cardItem",
  data() {
    return {
      apiGeneral: "https://pokeapi.co/api/v2/pokemon/",
      info: [],
      customInfo: [],
    };
  },
  methods: {
    /**
     **return just name & url of every single pokemon
     */
    getAllPokemon() {
      axios.get(this.apiGeneral).then((resp) => {
        this.info = resp.data.results;
      });
    },
    customPokemonData() {
      this.info.map((data) => {
        const urlSplited = data.url.split("/");
        const index = urlSplited[urlSplited.length - 2];
        const obj = {
          name: data.name,
          id: index,
          url: this.apiGeneral + index,
          img: "",
        };
        axios.get(obj.url).then((resp) => {
          obj.img = resp.data.sprites.other.dream_world.front_default;
        });
        return this.customInfo.push(obj);
      });
    },
  },
  beforeMount() {
    this.getAllPokemon();
  },
  created() {},
  mounted() {
    this.customPokemonData();
  },
};
</script>
<style>
/* @import "~bootstrap/dist/css/bootstrap.css"; */
</style>