<template>
  <div class="bg-black">
    <div class="container">
      <div class="detail">
        <!-- <img src="../assets/background.jpg" alt="" /> -->
        <div class="box-detail">
          <h1>{{ name }}</h1>
          <img :src="pokemon.front" alt="Pokemon" />

          <h2>
            weight : <span>{{ pokemon.w }} lb</span>
          </h2>
          <h2>
            height : <span>{{ pokemon.height * Math.floor(0.1) }} m</span>
          </h2>
          <h2>
            type : <span>{{ pokemon.typesN }}</span>
          </h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PokemonDetail",
  data() {
    return {
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
        this.pokemon.w = this.pokemon1.weight;
        this.pokemon.height = this.pokemon1.height;
        this.pokemon1.types.forEach((type) => {
          this.pokemon.typesN = type.type.name;
          console.log(this.pokemon.typesN);
        });
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style scoped>
.bg-black {
  height: 100vh;
}
.detail {
  text-align: center;
}
.box-detail {
  background-color: rgba(255, 255, 255, 0.117);
  backdrop-filter: blur(11px);
  margin-top: 66px;
  display: inline-block;
  width: -webkit-fill-available;
  padding: 40px;
  border: solid #ffc107;
  border-radius: 20px;
}
h1 {
  color: white;
}
h2 {
  text-align: start;
  color: rgb(255, 255, 255);
}
span {
  color: bisque;
}
img {
  width: 100px;
  height: auto;
}
</style>
