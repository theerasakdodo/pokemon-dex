<template>
  <div class="pokemon">
    <h1>PoKeDex</h1>

    <div class="container">
      <form @submit.prevent="searchPokemons">
        <b-form-input
          type="search"
          required
          v-model="search"
          placeholder="Search Pokemon..."
          @keydown="searchPokemons"
        />
      </form>
      <b-row cols="2" cols-sm="2" cols-md="4" cols-lg="4">
        <div v-for="(poke, index) in pokemonAPI" :key="poke">
          <PokemonDex :num="index + 1" :name="poke.name" :url="poke.url" /></div
      ></b-row>
    </div>
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
      search: "",
      pokemonSearch: "",
      pokemonAPI: [],
    };
  },

  created() {
    axios
      .get(`https://pokeapi.co/api/v2/pokemon?offset=200&limit=200`)
      .then((res) => {
        this.pokemonAPI = res.data.results;
        this.pokemonSearch = this.pokemonAPI;
        // console.log(res.data);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    searchPokemons: function () {
      this.pokemonAPI = this.pokemonSearch;
      if (this.search == "") {
        this.pokemonAPI = this.pokemonSearch;
      } else {
        this.pokemonAPI = this.pokemonSearch.filter((pokemon) =>
          pokemon.name.toLowerCase().includes(this.search.toLowerCase())
        );
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  text-align: center;
  padding: 20px 0px;
  color: white;
}
.pokemon {
  /* background-color: #000000f2; */
  background: linear-gradient(
    80deg,
    rgba(2, 0, 36, 1) 0%,
    rgba(1, 1, 9, 1) 35%,
    rgb(0 85 103) 100%
  );
}
</style>
