<template>
  <b-card class="mb-4 card-test">
    <!-- <div class="top-card"></div> -->
    <h1>{{ namePokemon.toUpperCase() }}</h1>
    <img
      :src="imgPokemon"
      alt=""
      @mouseenter="setImg"
      @mouseleave="setImg"
      class="cursor"
    />

    <!-- <img :src="pokemon.back" alt="" /> -->
    <router-link
      :to="{
        name: 'PokemonDetail',
        params: { name: this.name, data: this.url },
      }"
      ><b-button class="bt-max">Detail</b-button></router-link
    >
  </b-card>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDex",

  data() {
    return {
      isFront: true,
      imgPokemon: "",
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
  methods: {
    setImg: function () {
      if (this.isFront) {
        this.isFront = false;
        this.imgPokemon = this.pokemon.back;
      } else {
        this.isFront = true;
        this.imgPokemon = this.pokemon.front;
      }
    },
  },
  created() {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon = res.data;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.imgPokemon = this.pokemon.front;
        // console.log(this.pokemonData);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>
<style scoped>
h1 {
  color: white;
  text-align: center;
  height: 40px;
  font-size: calc(1rem);
}
img {
  width: 100%;
  height: auto;
}
img:hover {
  cursor: pointer;
}
.top-card {
  position: absolute;
}
.card-test {
  background-color: #0027ff36;
  -webkit-backdrop-filter: blur(30px);
  backdrop-filter: blur(30px);
  border: solid rgb(13 110 253);
  box-shadow: inset 0px 0px 6px #86b7fe;
}
.card-test:hover {
  box-shadow: none;
  border: solid #000000;
  background-color: #000000;
}
.bt-max {
  width: -webkit-fill-available;
  transition: 0.3s ease-in-out 0s;
  background-color: #6c757d;
}
.bt-max:hover {
  background-color: red;
  color: white;
  backdrop-filter: blur(30px);
  box-shadow: 0px 0px 1px 1px #ffffff38;
  transform: scale(1.02);
}
@media only screen and (max-width: 375px) {
  h1 {
    font-size: 12px;
  }
  .bt-max {
    font-size: 12px;
  }
}
</style>
