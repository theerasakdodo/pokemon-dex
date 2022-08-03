<template>
  <div>
    <h1>{{ namePokemon }}</h1>
    <img :src="pokemon.front" alt="" />
    <router-link to="/">
      <b-button>Home</b-button>
    </router-link>
  </div>
</template>
<script>
export default {
  name: "PokemonDetail",

  data() {
    return {
      datapoke: {},

      pokemon: {
        front: "",
        name: "",
      },
    };
  },
  created() {
    this.datapoke = this.$route.params.datapoke;
    this.pokemon.front = this.datapoke.sprites.front_default;
    this.pokemon.name = this.datapoke.name;
    console.log(this.pokemon.name);
  },
  computed: {
    namePokemon: function () {
      let newName =
        this.pokemon.name[0].toUpperCase() + this.pokemon.name.slice(1);
      return newName;
    },
  },
};
</script>
