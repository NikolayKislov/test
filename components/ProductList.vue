<template>
  <section class="product-list">
    <ProductListItem
      v-for="item in listItems"
      :key="item.id"
      :image="item.image"
      :title="item.title"
      :description="item.description"
      :price="item.price"
    />
  </section>
</template>

<script>
export default {
name: 'ProductList',
  props: {
  listItems: {
    type: Array,
    default() {
      return [];
    }
  },
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/media';

.product-list {
  max-width: 1028px;
  margin-top: 5px;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 20px 0;
  @include media.lg-up {

  }
  @include media.xl-only {
  }
}
</style>
