<template>
  <div class="px-4 py-2">
    <form>
      <input
        type="text"
        class="w-100 px-2"
        v-model="query"
        @keyup.enter="searchPokemon(query)"
      />
      <img
        @click="searchPokemon(query)"
        src="../assets/search.png"
        width="23"
        alt=""
      />
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: ''
    };
  },
  methods: {
    searchPokemon(query) {
      this.$emit('searchPokemon', query);
    }
  }
};
</script>
<style lang="scss" scoped>
input {
  font-size: 16px;
  font-family: 'Acme', arial, sans-serif;
  border-radius: 0.3rem;
  position: relative;
  height: 2rem;
}
img {
  cursor: pointer;
  top: 2.9rem;
  right: 2rem;
  position: absolute;
}
</style>