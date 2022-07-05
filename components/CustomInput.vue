<template>
  <div>
    <input
      :id="id"
      :value="value"
      :class="classNames"
      :maxlength="maxlength"
      type="text"
      :name="name"
      :placeholder="placeholder"
      @input="onChange($event)"
      @focus="onFocus"
      @blur="onBlur">
    <p v-show="isFocused && error" class="warning">{{ error }}</p>
  </div>
</template>

<script>
export default {
  name: 'CustomInput',
  props: {
    value: {
      type: String,
      default: '',
    },
    placeholder: {
      type: String,
      default: '',
    },
    name: {
      type: String,
      default: '',
    },
    id: {
      type: String,
      default: '',
    },
    maxlength: {
      type: String,
      default: '',
    },
    error: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      isFocused: false
    }
  },
  computed: {
    classNames() {
      const baseClass = 'item__input';

      if (this.isFocused) {
        return this.error ? `${baseClass} item__input--reject` : `${baseClass} item__input--allow`
      }

      return baseClass
    }
  },
  methods: {
    onChange(e) {
      this.$emit("input", e.target.value);
    },
    onFocus() {
      this.isFocused = true;
    },
    onBlur() {
      this.isFocused = false;
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

.item__input {
  box-sizing: border-box;
  width: 284px;
  height: 35px;
  padding: 10px 16px 11px;
  border-radius: var(--b-radius);
  border: none;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  background-color: var(--c-grey10);
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  font-family: var(--f-base);
  margin-top: 4px;
  transition: all ease-in-out .3s;

  &--allow {
    outline: 1px solid var(--c-primary);
  }

  &--reject {
    outline: 1px solid var(--c-secondary);

    &:focus,
    &:hover {
      outline: 1px solid var(--c-secondary);
    }
  }
}

.warning {
  font-size: 10px;
  margin: 4px 0 0 0;
  padding: 0;
  color: var(--c-secondary);
  transition: all ease-in-out .3s;
}
</style>
