<template>
  <div class="home">
    <header class="text-white text-center fs-lg py-2">Pokemon's</header>
    <pokemon-list />
  </div>
</template>

<script>
import PokemonList from "./PokemonList";
export default {
  components: {
    PokemonList
  },
  data() {
    return {};
  }
};
</script>

<style lang="scss" scoped>
.home {
  min-height: 100vh;
  background: radial-gradient(
    ellipse at center,
    rgba(7, 77, 119, 1) 0%,
    rgba(7, 52, 92, 1) 100%
  );
}
</style>