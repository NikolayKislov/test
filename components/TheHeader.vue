<template>
  <header class="header">
    <div class="header__container">
      <div class="header__logo">
        <h1 class="H1">Добавление товара</h1>
      </div>
      <div class="header__select-container">
        <client-only>
          <CustomSelect
            :options="options"
            :selected="selected"
            @select="optionSelect"
          />
        </client-only>
      </div>
    </div>
  </header>
</template>

<script>
import CustomSelect from "./CustomSelect"

export default {
  name: 'TheHeader',
  components: {
    CustomSelect,
  },
  data() {
    return {
      options: [
        {
          name: 'По умолчанию',
          value: 0
        },
        {
          name: 'По цене ↑',
          value: 1
        },
        {
          name: 'По цене ↓',
          value: 2
        },
        {
          name: 'По названию',
          value: 3
        },
      ],
      selected: 'По умолчанию'
    }
  },
  methods: {
    optionSelect(option) {
      this.selected = option.name
      this.$emit('sortingOrder', option.value)
    }
  }
}
</script>

<style lang="scss" scoped>
@use '@/assets/styles/helpers/helpers';
@use '@/assets/styles/helpers/vars';
@use '@/assets/styles/helpers/grid';
@use '@/assets/styles/helpers/media';
@use '@/assets/styles/helpers/heading';

.header__container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  @include media.sm-up {
    flex-direction: row;
  }
}

.select-container__select {
  width: 121.49px;
  height: 36px;
  margin-top: 10px;
  padding: 0 15px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: var(--b-radius);
  background-color: var(--c-grey10);
  outline: none;
  border: none;
  color: var(--c-grey30);
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
}
</style>
