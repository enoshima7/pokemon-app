<template>
  <div class="detail d-flex ai-center jc-center">
    <div
      class="container bg-white d-flex flex-column jc-center ai-center mx-4 w-100"
    >
      <img
        :src="imgURL + (pokemonId || pokemonData.id) + '.png'"
        alt=""
        class="bg-grey avatar d-flex ai-center jc-center"
      />
      <div class="data w-100 d-flex  flex-column mt-5 px-4 ">
        <div class="fs-md text-center">{{ pokemonData.name }}</div>
        <div class="d-flex jc-between ai-center bb w-100 mb-2">
          <span class="">Base Experience</span>
          <span>{{ pokemonData.base_experience }} XP</span>
        </div>
        <div class="d-flex jc-between ai-center bb w-100 mb-2">
          <span class="">Height</span>
          <span>{{ pokemonData.height }} m</span>
        </div>
        <div class="d-flex jc-between ai-center bb w-100 mb-2">
          <span class="">Weight</span>
          <span>{{ pokemonData.weight }} kg</span>
        </div>
        <div class="mt-3">
          <div class="bb mb-2">Pokemon Types</div>
          <div class="type-container">
            <span
              v-for="(type, i) in pokemonData.types"
              :key="i"
              class="type bg-blue-1 text-white px-2 py-1 mr-2"
              >{{ type.type.name }}</span
            >
          </div>
        </div>
        <div class="mt-3">
          <div class="bb mb-2">Abilities</div>
          <div class="type-container">
            <span
              v-for="(ability, i) in pokemonData.abilities"
              :key="i"
              class="type bg-orange text-white px-2 py-1 mr-2"
              >{{ ability.ability.name }}</span
            >
          </div>
        </div>
      </div>
      <div
        class="close bg-grey px-3 py-2 text-white mt-5 mb-3"
        @click="closeDetail"
      >
        close
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemonId: { type: String },
    pokemonName: { type: String }
  },
  watch: {
    pokemonName: function() {
      this.fetchPokemonDetail();
    }
  },
  methods: {
    async fetchPokemonDetail() {
      let res;
      if (this.pokemonId) {
        res = await this.$http.get(`${this.pokemonId}`);
      } else {
        res = await this.$http.get(`${this.pokemonName}`);
      }
      this.pokemonData = res.data;
      this.$emit('showDetailComp');
    },
    closeDetail() {
      this.$emit('closeDetail');
    }
  },
  data() {
    return {
      imgURL:
        'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
      pokemonData: {}
    };
  },
  created() {
    this.fetchPokemonDetail();
  }
};
</script>

<style lang="scss" scoped>
.detail {
  position: fixed;
  top: 0;
  left: 0;
  min-width: 100%;
  min-height: 100vh;
  background: rgba(0, 0, 0, 0.7);
  .container {
    border-radius: 0.4rem;
    position: relative;
    .avatar {
      position: absolute;
      border-radius: 50%;
      top: -60px;
    }
    .data {
      .type {
        border-radius: 1rem;
      }
    }
    .close {
      border-radius: 0.4rem;
      cursor: pointer;
    }
  }
}
</style>