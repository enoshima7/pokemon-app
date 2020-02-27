<template>
  <div class="home">
    <div class="title bg-blue-1">
      <header class=" text-white text-center fs-lg py-2">Pokemon's</header>
      <pokemon-search @searchPokemon="searchPokemon" class="searchBar" />
    </div>
    <pokemon-list @passID="passID" />
    <transition-group>
      <pokemon-detail
        key="detail"
        @showDetail="showDetailComp"
        :pokemonName="query"
        :pokemonId="id"
        v-if="showDetail"
        @closeDetail="closeDetail"
      />

      <pokemon-error key="error" v-if="showError" @closeDetail="closeDetail" />
    </transition-group>
  </div>
</template>

<script>
import PokemonList from './PokemonList';
import PokemonDetail from './PokemonDetail';
import PokemonSearch from './PokemonSearch';
import PokemonError from './PokemonError';
export default {
  components: {
    PokemonList,
    PokemonSearch,
    PokemonDetail,
    PokemonError
  },
  data() {
    return {
      id: '',
      showDetail: false,
      showError: false,
      query: ''
    };
  },
  methods: {
    showDetailComp() {
      this.showDetail = true;
    },

    async searchPokemon(query) {
      try {
        query = query.toLowerCase();
        this.query = query;
        this.id = '';
        await this.$http.get(`${query}`);
        this.showDetail = true;
      } catch (error) {
        this.showError = true;
      }
    },
    passID(id) {
      this.id = id;
      this.showDetail = true;
    },
    closeDetail() {
      this.showDetail = false;
      this.showError = false;
    }
  }
};
</script>

<style lang="scss" scoped>
.title {
  position: sticky;
  top: 0;
  z-index: 999;
}
.home {
  min-height: 100vh;
  background: radial-gradient(
    ellipse at center,
    rgba(7, 77, 119, 1) 0%,
    rgba(7, 52, 92, 1) 100%
  );
}
.v-enter-active {
  transition: all 0.3s ease;
}
.v-leave-active {
  transition: all 0.3s ease;
}
.v-enter, .v-leave-to
/* .slide-fade-leave-active for below version 2.1.8 */ {
  transform: translateY(-10px);
  opacity: 0;
}
</style>