<template>
  <div>
    <div class="container d-flex ai-center flex-wrap">
      <div
        class="pokemon-item bg-white text-center d-flex flex-column ai-center my-2 ml-4"
        v-for="(item, index) in pokemons"
        :key="index"
      >
        <img width="96" height="96" :src="imgURL + item.id + '.png'" alt="" />
        <span class="pb-2">
          {{ item.name }}
        </span>
      </div>
      <div
        class="my-2 ml-4 d-flex ai-center jc-center"
        style="width: 8rem;"
        ref="scrollTrigger"
      >
        <img src="../assets/spinner.png" class="spinner" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemons: [],
      currentURL: "",
      nextURL: "",
      imgURL:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/"
    };
  },
  methods: {
    async fetchPokemons() {
      const res = await this.$http.get("/");
      this.pokemons = res.data.results;
      this.pokemons.map(v => {
        v.id = v.url
          .split("/")
          .filter(v => !!v)
          .pop();
      });
    }
  },
  created() {
    this.fetchPokemons();
  }
};
</script>

<style lang="scss" scoped>
.container {
  .pokemon-item {
    width: 8rem;
    border-radius: 1.3rem;
    box-shadow: 0px 6px 10px -2px rgba(0, 0, 0, 0.24);
    cursor: pointer;
  }
  .spinner {
    width: 3.8462rem;
    animation: spin 2000ms infinite linear;
  }
}
</style>