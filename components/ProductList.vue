<template>
  <section class="product-list">
    <ProductListItem
      v-for="item in listItems"
      :id="item.id"
      :key="item.id"
      :image="item.image"
      :title="item.title"
      :description="item.description"
      :price="item.price"
      @sendId="sendId"
    />
  </section>
</template>

<script>
import ProductListItem from "@/components/ProductListItem";

export default {
  name: 'ProductList',
  components: {
    ProductListItem
  },
  props: {
    listItems: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      itemId: ''
    }
  },
  methods: {
    sendId(value) {
      this.$emit('sendID', value)
    }
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/media';

.product-list {
  max-width: 1028px;
  margin-top: 5px;
  width: 100%;
  display: grid;
  grid-template-columns: 1fr;
  justify-content: center;
  align-content: center;
  place-items: center;
  gap: 19px 16px;
  @include media.lg-to-xl {
    grid-template-columns: repeat(2, 1fr);
    max-width: 800px;
  }
  @include media.xl-only {
    grid-template-columns: repeat(3, 1fr);
    max-width: 1028px;
  }
}
</style>
