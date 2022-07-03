<template>
  <main class="main">
    <TheForm @onAddItem="handleAddItem"/>
    <ProductList
      @sendID="deleteItemFromList"
      :list-items="listItems"/>
  </main>
</template>

<script>
import TheForm from "~/components/TheForm";
import ProductList from "@/components/ProductList";
export default {
  name: 'TheMain',
  components: {
    TheForm,
    ProductList
  },
  data() {
    return {
      listItems: []
    }
  },
  methods: {
    handleAddItem(item) {
      this.listItems.push({...item})
    },
    deleteItemFromList(value) {
      this.listItems = this.listItems.filter(el => el.id !== value)
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
