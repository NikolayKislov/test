<template>
  <aside class="form-section">
    <form action="addToList">
      <form class="form">
        <div class="form__item">
          <label for="name" class="item__label">Наименование товара</label><br>
          <input
            id="name"
            v-model="listItem.title"
            class="item__input"
            type="text"
            name="name"
            placeholder="Введите наименование товара"><br>
        </div>
        <div class="form__item">
          <label for="textarea" class="item__label">Описание товара</label>
          <textarea
            id="textarea"
            v-model="listItem.description"
            class="item__textarea"
            name="textarea"
            placeholder="Введите описание товара"></textarea>
        </div>
        <div class="form__item">
          <label for="link" class="item__label">Ссылка на изображение товара</label><br>
          <input
            id="link"
            v-model="listItem.image"
            class="item__input"
            type="text" name="link"
            placeholder="Введите ссылку">
        </div>
        <div class="form__item">
          <label for="price" class="item__label">Цена товара</label><br>
          <input
            id="price"
            v-model="fValue"
            class="item__input"
            type="text"
            name="price"
            placeholder="Введите цену">
        </div>
        <button class="btn" :class="{'btn--allow': checkEmptyFields}" type="submit" @click.prevent="addItem">Добавить
          товар
        </button>
      </form>
    </form>
  </aside>
</template>

<script>
export default {
  name: 'TheForm',
  data() {
    return {
      listItem: {
        image: '',
        title: '',
        description: '',
        price: ''
      },
      price: ''
    }
  },
  computed: {
    checkEmptyFields() {
      return this.listItem.image !== '' && this.listItem.title !== '' && this.listItem.price !== '';
    },
    fValue: {
      // getter
      get() {
        return this.listItem.price;
      },
      // setter
      set(newValue) {
        if (newValue.length > 3) {
          newValue = newValue.replace(" ", "");
          this.listItem.price =
            newValue.substr(0, newValue.length - 3) +
            " " +
            newValue.substr(newValue.length - 3);
        } else {
          this.listItem.price = newValue;
        }
      }
    }
  },
  methods: {
    addItem() {
      this.$emit('onAddItem', this.listItem)
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

.form-section {
  width: 330px;
  height: 436px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: var(--b-radius);
}

.form {
  margin-left: 20px;
  padding-top: 14px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  font-family: var(--f-base);
  color: var(--c-grey30);
  gap: 11px;
}

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

  &:focus,
  &:hover {
    outline: 1px solid var(--c-primary);
  }
}

.item__label {
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  font-family: var(--f-base);
  color: var(--c-grey50);
}

.item__textarea {
  display: block;
  resize: none;
  width: 284px;
  height: 108px;
  padding: 14px 16px 11px;
  border-radius: var(--b-radius);
  border: none;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  background-color: var(--c-grey10);
  font-weight: 400;
  font-size: 12px;
  line-height: 15px;
  font-family: var(--f-base);
  margin-top: 0;

  &:focus,
  &:hover {
    outline: 1px solid var(--c-primary);
  }
}

.btn {
  cursor: pointer;
  margin-top: 14px;
  width: 284px;
  height: 36px;
  background: var(--c-grey20);
  border-radius: 10px;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  text-align: center;
  letter-spacing: -0.02em;
  color: var(--c-grey30);
  border: none;

  &--allow {
    background: var(--c-primary);
    color: var(--c-grey00);

    &:hover {
      background-color: var(--c-primary-dark);
    }
  }
}
</style>
