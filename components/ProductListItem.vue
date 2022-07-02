<template>
  <div class="product-item">
    <img class="product-item__image" :src="`${image}`" :alt="`${title}`">
    <h2 class="H2">{{ title }}</h2>
    <p class="product-item__description">{{ description }}</p>
    <p class="product-item__price H2">{{ price }}</p>
  </div>
</template>

<script>
export default {
  name: 'ProductListItem',
  props: {
    image: {
      type: String,
      default: '',
    },
    title: {
      type: String,
      default: '',
    },
    description: {
      type: String,
      default: '',
    },
    price: {
      type: String,
      default: '',
    },
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/helpers';
@use '@/assets/styles/helpers/vars';
@use '@/assets/styles/helpers/grid';
@use '@/assets/styles/helpers/media';
@use '@/assets/styles/helpers/heading';

.product-item {
  max-width: 332px;
  width: 100%;
  min-height: 420px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  background: var(--c-grey10);
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.04), 0 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: var(--b-radius);
  font-family: var(--f-base);
  color: var(--c-grey40);
}

.product-item__image {
  max-width: inherit;
  width: 100%;
  min-height: 180px;
  border-top-left-radius: var(--b-radius);
  border-top-right-radius: var(--b-radius);
}

.product-item__description {
  margin: 0;
  padding: 0;
  max-width: 300px;
  width: 100%;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  overflow-wrap: break-word;
}

.product-item__price {
  align-self: flex-start;
  padding-left: 20px;
}
</style>
