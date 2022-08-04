<template>
  <b-container>
    <div class="bg-bl">
      <img :src="pokemon.front" alt="Pokemon" />
      <h3>{{ name }}</h3>
    </div>
  </b-container>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDetail",
  data() {
    return {
      data: {},
      pokemon: {},
    };
  },
  created: function () {
    this.data1 = this.$route.params;

    this.name = this.data1.name;

    axios
      .get(this.data1.data)
      .then((res) => {
        this.pokemon1 = res.data;
        this.pokemon.front = this.pokemon1.sprites.front_default;
        console.log(this.pokemon.front);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style scoped>
.bg-bl {
  color: #000;
}
</style>
