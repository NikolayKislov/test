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
      this.listItems.push(item)
    }
  }
}
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: space-between;
}
</style>
