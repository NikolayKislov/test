<template>
  <div class="custom-select">
    <p
      @click="areOptionsVisible = !areOptionsVisible"
    >{{ selected }}   <span class="arrow"></span></p>

    <div
      v-if="areOptionsVisible"
      class="options"
    >
      <p
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CustomSelect',
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      areOptionsVisible: false,
    }
  },
  methods: {
    selectOption(option) {
      this.$emit('select', option)
      this.areOptionsVisible = false
    },
    hideSelect() {
      this.areOptionsVisible = false
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

.custom-select {
  width: 121px;
  height: 36px;
  margin-top: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: var(--b-radius);
  background-color: var(--c-grey10);
  outline: none;
  border: none;
  color: var(--c-grey30);
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  position: relative;

}

p {
  padding: 11px 13px 10px 10px;
  cursor: pointer;
  border-radius: var(--b-radius);

  &:hover {
    background: var(--c-grey20);
  }
}
.arrow {
  width: 5px;
  height: 5px;
  transform: rotate(45deg);
  border-right:1px solid var(--c-grey30);
  border-bottom: 1px solid var(--c-grey30);
  position: absolute;
  right: 12px;
  top: 15px;
}
.options {
  position: absolute;
  top: 40px;
  left: 0;
  width: inherit;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: var(--b-radius);
  background-color: var(--c-grey10);
  outline: none;
  border: none;
  color: var(--c-grey30);
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
}
</style>
