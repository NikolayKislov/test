<template>
  <main class="main">
    <TheForm @onAddItem="handleAddItem"/>
    <ProductList :list-items="listItems"/>
  </main>
</template>

<script>
import TheForm from "~/components/TheForm";

export default {
  name: 'TheMain',
  components: {
    TheForm
  },
  data() {
    return {
      listItems: []
    }
  },
  methods: {
    handleAddItem(item) {
      this.listItems.push({...item})
    }
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/media';
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  max-width: 1400px ;
  @include media.md-up {
    flex-direction: row;
    align-items: flex-start;
  }
}
</style>
