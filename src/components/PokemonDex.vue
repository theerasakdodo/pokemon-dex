<template>
  <b-card>
    <h1>{{ namePokemon }}</h1>
    <img :src="pokemonImg" alt="" />
  </b-card>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDex",

  data() {
    return {
      pokemonImg: "",
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
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemonImg = this.pokemon.front;
        console.log(res);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>
<style scoped></style>
