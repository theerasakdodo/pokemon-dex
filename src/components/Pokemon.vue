<template>
  <div class="pokemon container">
    <h1>PoKeDex</h1>
    <b-row cols="3">
      <div v-for="(poke, index) in pokemonAPI" :key="poke">
        <PokemonDex :num="index + 1" :name="poke.name" :url="poke.url" /></div
    ></b-row>
  </div>
</template>

<script>
import axios from "axios";
import PokemonDex from "./PokemonDex.vue";
export default {
  name: "Pokemon",
  components: {
    PokemonDex,
  },
  data() {
    return {
      pokemonAPI: [],
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon")
      .then((res) => {
        this.pokemonAPI = res.data.results;
        // console.log(res.data);
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
