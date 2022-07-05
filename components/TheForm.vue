<template>
  <aside class="form-section">
    <form class="form">
      <div class="form__item">
        <label for="name" class="item__label">Наименование товара</label><br>
        <CustomInput
          id="name"
          v-model="listItem.title"
          maxlength="20"
          type="text"
          name="name"
          placeholder="Введите наименование товара"
          :error="isNameValid"
        />
        <br>
      </div>
      <div class="form__item">
        <label for="textarea" class="text__label">Описание товара</label>
        <textarea
          id="textarea"
          v-model="listItem.description"
          class="item__textarea"
          maxlength="118"
          name="textarea"
          placeholder="Введите описание товара"></textarea>
      </div>
      <div class="form__item">
        <label for="link" class="item__label">Ссылка на изображение товара</label><br>
        <CustomInput
          id="link"
          v-model="listItem.image"
          type="text" name="link"
          placeholder="Введите ссылку"
          :error="isLinkValid"
        />
      </div>
      <div class="form__item">
        <label for="price" class="item__label">Цена товара</label><br>
        <CustomInput
          id="price"
          v-model="fValue"
          type="text"
          name="price"
          placeholder="Введите цену"
          :error="isPriceValid"
        />
      </div>
      <button
        class="btn"
        :class="{'btn--allow': isFormValid, 'btn--disabled': !isFormValid}"
        type="submit"
        @click.prevent="addItem">Добавить
        товар
      </button>
    </form>
  </aside>
</template>

<script>
import CustomInput from "~/components/CustomInput";

export default {
  name: 'TheForm',
  components: {
    CustomInput,
  },
  data() {
    return {
      listItem: {
        id: '',
        image: '',
        title: '',
        description: '',
        price: ''
      },
      exp: /(http[s]*:\/\/)([a-z\-\d/.]+)\.([a-z.]{2,3})\/([a-z\d\-_/.~:?#[\]@!$&'()*+,;=%]*)([a-z\d]+\.)(jpg|jpeg|png)/i,
      isValid: true
    }
  },
  computed: {
    fValue: {
      // getter
      get() {
        return this.listItem.price;
      },
      // setter
      set(n) {
        this.listItem.price = [...n.replaceAll(" ", "")].reverse().reduce((acc, v, i) => [...acc, ...((i - 2) % 3 === 0 && i > 0 ? [v, ' '] : [v])], []).reverse().join('').trim();
      }
    },
    isNameValid() {
      return !this.listItem.title ? 'Поле является обязательным' : ''
    },
    isLinkValid() {
      return !this.listItem.image ? 'Поле является обязательным' : !this.listItem.image.match(this.exp) ? 'Невалидная ссылка' : ''
    },
    isPriceValid() {
      return !this.listItem.price ? 'Поле является обязательным' : isNaN(+this.listItem.price.replaceAll(' ', '')) ? 'Поле может содержать только цифры' : ''
    },
    isFormValid() {
      return !(this.isNameValid || this.isLinkValid || this.isPriceValid)
    }
  },
  methods: {
    addItem() {
      if (this.listItem.image !== '' && this.listItem.title !== '' && this.listItem.price !== '' && this.listItem.image.match(this.exp)) {
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

.item__label,
.text__label {
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
