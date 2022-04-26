<template>
  <div class="product-form">
    <div class="product-form__header">
      <h2 class="product-form__title">
        Добавление товара
      </h2>
      <select id="" class="product-form__header-select" name="">
        <option value="По умолчанию">
          По умолчанию
        </option>
        <option value="" />
        <option value="" />
      </select>
    </div>
    <div class="product-form__container">
      <form class="product-form__form" @submit.prevent="submitForm" @change="checkValid">
        <label class="product-form__form_req" for="name">
          <span>Наименование товара</span>
          <input
            id="name"
            v-model="name"
            :class="`${!nameValid ? 'product-form__input_invalid' : ''}`"
            type="text"
            placeholder="Введите наименование товара"
            @input="checkValid"
          >
          <p v-show="!nameValid" class="product-form__form_req-text">Поле является обязательным</p>
        </label>
        <label for="description">
          <span>Описание товара</span>
          <textarea id="description" v-model="description" placeholder="Введите описание товара" />
        </label>
        <label class="product-form__form_req" for="link">
          <span>Ссылка на изображение товара</span>
          <input
            id="link"
            v-model="link"
            :class="`${!linkValid ? 'product-form__input_invalid' : ''}`"
            type="text"
            placeholder="Введите ссылку"
            @input="checkValid"
          >
          <p v-show="!linkValid" class="product-form__form_req-text">Поле является обязательным</p>
        </label>
        <label class="product-form__form_req" for="price">
          <span>Цена товара</span>
          <input
            id="price"
            v-model="price"
            :class="`${!priceValid ? 'product-form__input_invalid' : ''}`"
            placeholder="Введите цену"
            v-bind="price | formattedPrice"
            @input="checkValid"
          >
          <p v-show="!priceValid" class="product-form__form_req-text">Поле является обязательным</p>
        </label>
        <button
          type="submit"
          :class="`product-form__button ${IsValid ? '' : 'product-form__button_disabled'}`"
          :disabled="!IsValid"
        >
          Добавить товар
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import formattedPrice from '../filters/price-format.js'
export default {
  name: 'ProductForm',
  filters: {
    formattedPrice
  },
  data () {
    return {
      name: '',
      description: '',
      link: '',
      price: '',
      nameValid: true,
      linkValid: true,
      priceValid: true,
      isValid: false
    }
  },
  methods: {
    clearForm () {
      this.name = ''
      this.description = ''
      this.link = ''
      this.price = ''
      this.nameValid = true
      this.linkValid = true
      this.priceValid = true
      this.isValid = false
    },
    submitForm () {
      const form = {
        id: Date.now(),
        name: this.name,
        description: this.description,
        link: this.link,
        price: this.price
      }
      this.$emit('submitForm', form)
      this.clearForm()
    },
    checkValid () {
      this.nameValid = !!this.name.length
      this.linkValid = !!this.link.length
      this.priceValid = !!this.price.length
      if (this.nameValid && this.linkValid && this.priceValid) {
        this.isValid = true
      } else {
        this.isValid = false
      }
    },
    formatPrice (value) {
      const val = (value / 1).toFixed(2).replace('.', ',')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, '.')
    }

  }
}
</script>

<style lang="scss">
.product-form {
    &__title {
        margin: 0;
        font-size: 28px;
        font-weight: 600;
        color: #3F3F3F;
    }
    &__container {
        max-width: 332px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        padding: 24px;
    }
    &__form {
        text-align: left;
      label {
        margin-bottom: 16px;
        display: block;
        color: #49485E;
      }
    &_req {
      span {
        position: relative;
        &:after {
          content: "";
          width: 4px;
          height: 4px;
          border-radius: 100%;
          background-color: #FF8484;
          position: absolute;
          top: 3px;
          right: -5px;
        }
      }
      &-text {
        font-weight: 400;
        color: #FF8484;
        margin: 4px 0 0;
        font-size: 12px;
      }
    }
  }
  input, textarea {
    color: #3F3F3F;
    font-weight: 400;
    font-size: 12px;
    line-height: 15px;
    border-radius: 4px;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    padding: 10px 0 10px 16px;
    outline: none;
    border: 1px solid transparent;
    width: 100%;
    margin-top: 4px;
    box-sizing: border-box;
    transition: 0.3s;
    &::placeholder {
      color: #B4B4B4;
    }
    &:focus {
      border-color:#3F3F3F;
    }
  }
  &__input-invalid {
    border-color: #FF8484 !important;
  }
  textarea {
    min-height: 108px;
    max-height: 150px;
    resize: vertical;
  }
  &__button {
    background: #7BAE73;
    border-radius: 10px;
    color: #fff;
    font-size: 12px;
    font-weight: 600;
    width: 100%;
    padding: 11px 0;
    border: none;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    &_disabled {
      background: #EEEEEE;
      box-shadow: none;
      color: #B4B4B4;
      cursor: unset;
    }
    &_active {
      box-shadow: inset 1px 1px 10px #333;
    }
  }
  &__header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 16px;
    &-select {
      width: 100%;
      max-width: 122px;
      cursor: pointer;
      display: flex;
      justify-content: flex-end;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border: 1px solid transparent;
      padding: 10px 5px 10px 5px;
      border-radius: 4px;
      outline: none;
      font-size: 12px;
      color: #000;
      transition: 0.3s;
      &:focus {
        border-color: #3F3F3F;
      }
      &::placeholder {
        color: #B4B4B4;
      }
    }
      option {
        font-style: normal;
        font-weight: 400;
        font-size: 12px;
        line-height: 15px;
        color: #B4B4B4;
      }
    }
  }

</style>
