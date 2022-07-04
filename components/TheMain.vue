<template>
  <main class="main">
    <TheForm @onAddItem="handleAddItem"/>
    <ProductList
      :list-items="listItems"
      @sendID="deleteItemFromList"
    />
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
  props: {
    sortOrder: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      listItems: [],
      sortIndex: 0
    }
  },
  watch: {
    '$props': {
      handler(val) {
        this.sortIndex = val
        if (val.sortOrder === 1) {
          return this.listItems.sort((a, b) => a.price.replaceAll(" ", '').replace(/'\d'/g, '') - b.price.replaceAll(" ", '').replace(/'\d'/g, ''));
        }
        if (val.sortOrder === 2) {
          return this.listItems.sort((a, b) => b.price.replaceAll(" ", '').replace(/'\d'/g, '') - a.price.replaceAll(" ", '').replace(/'\d'/g, ''));
        } else {
          return this.listItems.sort((a, b) => a.title.replaceAll(" ", '').localeCompare(b.title.replaceAll(" ", '')));
        }
      },
      deep: true
    }
  },
  methods: {
    handleAddItem(item) {
      this.listItems.push({...item})
    },
    deleteItemFromList(value) {
      this.listItems = this.listItems.filter(el => el.id !== value)
    }
  },
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/media';

.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  gap: 18px;
  max-width: 1400px;
  @include media.md-up {
    justify-content: center;
    gap: 5px;
    flex-direction: row;
    align-items: flex-start;
  }
  @include media.xl-only {
    justify-content: space-between;
    gap: 18px;
  }
}
</style>
