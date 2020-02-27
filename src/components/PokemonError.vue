<template>
  <div class="error  d-flex ai-center jc-center">
    <div class="wrapper bg-white d-flex ai-center flex-column w-100 mx-5 py-4">
      <div class="d-flex ai-center pb-2 bb">
        <img src="../assets/Error.png" width="50" alt="" class="" />
        <span class="fs-lg ml-3 ">404 NOT FOUND</span>
      </div>
      <div
        class="close bg-grey px-3 py-2 text-white mt-3 mb-2"
        @click="closeDetail"
      >
        close
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    closeDetail() {
      this.$emit('closeDetail');
    }
  }
};
</script>

<style lang="scss" scoped>
.error {
  position: fixed;
  top: 0;
  left: 0;
  min-width: 100%;
  min-height: 100vh;
  background: rgba(0, 0, 0, 0.7);
  .wrapper {
    border-radius: 0.5rem;
    box-shadow: -2px 21px 29px 3px rgba(0, 0, 0, 0.75);
  }
  .close {
    border-radius: 0.4rem;
    cursor: pointer;
  }
}
</style>