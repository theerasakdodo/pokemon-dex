<template>
  <b-card style="max-width: 20rem">
    <b-row col="3">
      <router-link
        :to="{
          name: 'PokemonDetail',
          params: { name: this.name, data: this.url },
        }"
      >
        <h1>{{ namePokemon }}</h1>
        <img :src="pokemon.front" alt="" /></router-link
    ></b-row>
  </b-card>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDex",

  data() {
    return {
      pokemonData: {},

      pokemon: {
        front: "",
      },
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  computed: {
    namePokemon: function () {
      let newName = this.name[0].toUpperCase() + this.name.slice(1);
      return newName;
    },
  },

  created() {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon = res.data;
        this.pokemon.front = res.data.sprites.front_default;

        // console.log(this.pokemonData);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>
<style scoped></style>
