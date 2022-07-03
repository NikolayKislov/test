<template>
  <aside class="form-section">
    <form class="form">
      <div class="form__item">
        <label for="name" class="item__label">Наименование товара</label><br>
        <input
          id="name"
          v-model="listItem.title"
          class="item__input"
          :class="`${listItem.title? 'item__input--allow' : 'item__input--reject'}`"
          maxlength="20"
          type="text"
          name="name"
          placeholder="Введите наименование товара"><br>
        <p v-show="listItem.title === ''" class="warning">Поле является обязательным</p>
      </div>
      <div class="form__item">
        <label for="textarea" class="text__label">Описание товара</label>
        <textarea
          id="textarea"
          v-model="listItem.description"
          class="item__textarea"
          maxlength="120"
          name="textarea"
          placeholder="Введите описание товара"></textarea>
      </div>
      <div class="form__item">
        <label for="link" class="item__label">Ссылка на изображение товара</label><br>
        <input
          id="link"
          v-model="listItem.image"
          class="item__input"
          :class="`${listItem.image.match(exp)? 'item__input--allow' : 'item__input--reject'}`"
          type="text" name="link"
          placeholder="Введите ссылку">
        <p v-show="listItem.image === ''" class="warning">Поле является обязательным</p>
        <p v-show="!listItem.image.match(exp) && listItem.image !== ''" class="warning">Невалидная ссылка</p>
      </div>
      <div class="form__item">
        <label for="price" class="item__label">Цена товара</label><br>
        <input
          id="price"
          v-model="fValue"
          class="item__input"
          :class="`${listItem.price? 'item__input--allow' : 'item__input--reject'}`"
          type="text"
          maxlength="7"
          name="price"
          placeholder="Введите цену">
        <p v-show="listItem.price === ''" class="warning">Поле является обязательным</p>
      </div>
      <button
        class="btn"
        :class="{'btn--allow': checkEmptyFields, 'btn--disabled': !checkEmptyFields}"
        type="submit"
        @click.prevent="addItem">Добавить
        товар
      </button>
    </form>
  </aside>
</template>

<script>
export default {
  name: 'TheForm',
  data() {
    return {
      listItem: {
        id: '',
        image: '',
        title: '',
        description: '',
        price: ''
      },
      exp: /(http[s]*:\/\/)([a-z\-\d/.]+)\.([a-z.]{2,3})\/([a-z\d\-_/.~:?#[\]@!$&'()*+,;=%]*)([a-z\d]+\.)(jpg|jpeg|png)/i
    }
  },
  computed: {
    checkEmptyFields() {
      const exp = /(http[s]*:\/\/)([a-z\-\d/.]+)\.([a-z.]{2,3})\/([a-z\d\-_/.~:?#[\]@!$&'()*+,;=%]*)([a-z\d]+\.)(jpg|jpeg|png)/i
      return this.listItem.image !== '' && this.listItem.title !== '' && this.listItem.price !== '' && this.listItem.image.match(exp)
    },
    fValue: {
      // getter
      get() {
        return this.listItem.price;
      },
      // setter
      set(n) {
        if (n.length > 3) {
          n = n.replace(" ", "");
          this.listItem.price =
            n.substr(0, n.length - 3) +
            " " +
            n.substr(n.length - 3);
        } else {
          this.listItem.price = n;
        }
      }
    }
  },
  methods: {
    addItem() {
      const exp = /(http[s]*:\/\/)([a-z\-\d/.]+)\.([a-z.]{2,3})\/([a-z\d\-_/.~:?#[\]@!$&'()*+,;=%]*)([a-z\d]+\.)(jpg|jpeg|png)/i
      if (this.listItem.image !== '' && this.listItem.title !== '' && this.listItem.price !== '' && this.listItem.image.match(exp)) {
        this.listItem.id = String(+new Date())
        this.$emit('onAddItem', this.listItem)
        this.listItem.title = ''
        this.listItem.description = ''
        this.listItem.image = ''
        this.listItem.price = ''
      }
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

.form-section {
  width: 332px;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: var(--b-radius);
}

.form {
  padding: 24px;
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

.item__label,
.text__label{
  font-weight: 400;
  font-size: 10px;
  line-height: 13px;
  letter-spacing: -0.02em;
  font-family: var(--f-base);
  color: var(--c-grey50);
  position: relative;
}

.item__label::after {
  content: '';
  width: 4px;
  height: 4px;
  position: absolute;
  border-radius: var(--b-radius-md);
  background-color: var(--c-secondary);
  top: 0;
  right: -6px;
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
  transition: all ease-in-out .5s;

  &--allow {
    cursor: pointer;
    background: var(--c-primary);
    color: var(--c-grey00);

    &:hover {
      background-color: var(--c-primary-dark);
    }
  }

  &--disabled {
    &:disabled {
      cursor: default;
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
