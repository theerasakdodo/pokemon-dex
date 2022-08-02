<template>
  <div v-for="(poke, index) in pokemonAPI" :key="poke.url">
    <PokemonDex :num="index + 1" :name="poke.name" :url="poke.url" />
  </div>
</template>

<script>
import axios from "axios";
import PokemonDex from "./PokemonDex.vue";
export default {
  name: "Pokemon",
  comments: {
    PokemonDex,
  },
  data() {
    return {
      pokemonAPI: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon")
      .then((res) => {
        this.pokemonAPI = res.data.results;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  text-align: center;
}
</style>
