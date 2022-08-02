<template>
  <div class="home">
    <Pokemon />
  </div>
</template>

<script>
// @ is an alias to /src
import Pokemon from "@/components/Pokemon.vue";

export default {
  name: "Home",
  components: {
    Pokemon,
  },
};
</script>
