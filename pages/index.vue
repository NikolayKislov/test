<template>
  <div class="app">
    <div class="container">
      <TheHeader
      @sortingOrder="getOrder"
      />
      <TheMain
      :sort-order="sortOption"
      />
    </div>
  </div>
</template>

<script>
import TheHeader from "~/components/TheHeader";
export default {
  name: 'IndexPage',
  components: {
    TheHeader
  },
  data() {
    return {
      sortOption: '',
    }
  },
  methods: {
    getOrder(value) {
      this.sortOption = value
    }
  }
}
</script>
<style lang="scss" scoped>
@use '@/assets/styles/helpers/helpers';
@use '@/assets/styles/helpers/grid';
@use '@/assets/styles/helpers/media';
</style>
