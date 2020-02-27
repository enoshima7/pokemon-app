<template>
  <div>
    <div class="container d-flex ai-center flex-wrap">
      <div
        @click="passID(item.id)"
        class="pokemon-item bg-white text-center d-flex flex-column ai-center my-2 ml-4"
        v-for="item in pokemons"
        :key="item.id"
      >
        <img width="96" height="96" :src="imgURL + item.id + '.png'" alt="" />
        <span class="pokemon-name pb-2">
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
      currentURL: '/',
      nextURL: '',
      imgURL:
        'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'
    };
  },

  methods: {
    passID(id) {
      this.$emit('passID', id);
    },
    lazyload() {
      const observer = new IntersectionObserver(entries => {
        entries.forEach(v => {
          if (v.intersectionRatio > 0 && this.nextURL) {
            this.fetchPokemons();
          }
        });
      });
      observer.observe(this.$refs.scrollTrigger);
    },
    async fetchPokemons() {
      const res = await this.$http.get(`${this.currentURL}`);
      this.nextURL = '/' + res.data.next.split('/').pop();
      res.data.results.map(v => {
        this.pokemons.push(v);
      });
      this.pokemons.map(v => {
        v.id = v.url
          .split('/')
          .filter(v => !!v)
          .pop();
      });
      this.currentURL = this.nextURL;
    }
  },
  created() {
    this.fetchPokemons();
  },
  mounted() {
    this.lazyload();
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
    transition: 0.3s all ease;
  }
  .pokemon-item:hover {
    transform: scale(1.1);
    box-shadow: 0px 20px 20px -5px rgba(0, 0, 0, 0.75);
  }

  .spinner {
    width: 3.8462rem;
    animation: spin 2000ms infinite linear;
  }
  .pokemon-name {
    text-transform: capitalize;
  }
}
</style>
