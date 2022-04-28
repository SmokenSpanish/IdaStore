<template>
  <div class="product-form">
    <h2 class="product-form__title">
      Добавление товара
    </h2>
    <div class="product-form__container">
      <form class="product-form__form" @submit.prevent="submitForm" @change="checkValid">
        <label class="product-form__form_req" for="title">
          <span>Наименование товара</span>
          <input
            id="title"
            v-model="title"
            maxlength="20"
            :class="`${!titleValid ? 'product-form__input_invalid' : ''}`"
            type="text"
            placeholder="Введите наименование товара"
            @input="checkValid"
          >
          <p v-show="!titleValid" class="product-form__form_req-text">Поле является обязательным</p>
        </label>
        <label for="description">
          <span>Описание товара</span>
          <textarea id="description" v-model="description" placeholder="Введите описание товара" :maxlength="limit" />
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
            :type="indicatorChange ? 'number' : 'text'"
            :class="`${!priceValid ? 'product-form__input_invalid' : ''}`"
            placeholder="Введите цену"
            @focus="indicatorChange = true"
            @blur="indicatorChange = false"
          >
          <p v-show="!priceValid" class="product-form__form_req-text">Поле является обязательным</p>
        </label>
        <button
          type="submit"
          :class="`product-form__button ${allValid ? '' : 'product-form__button_disabled'}`"
          :disabled="!allValid"
        >
          Добавить товар
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductForm',
  data () {
    return {
      title: '',
      description: '',
      link: '',
      limit: 120,
      realNumber: 0,
      indicatorChange: false,
      titleValid: true,
      linkValid: true,
      priceValid: true,
      allValid: false
    }
  },
  computed: {
    price: {
      get () {
        return this.indicatorChange ? this.realNumber : this.realNumber.toLocaleString()
      },
      set (value) {
        this.realNumber = +value.replace(/\s/g, '')
        this.$emit('input', this.realNumber)
      }
    }
  },
  created () {
    this.realNumber = this.value || ''
  },
  methods: {
    clearForm () {
      this.title = ''
      this.description = ''
      this.link = ''
      this.price = ''
      this.titleValid = true
      this.linkValid = true
      this.priceValid = true
      this.allValid = false
    },
    submitForm () {
      const form = {
        id: Date.now(),
        title: this.title,
        description: this.description,
        link: this.link,
        price: this.price
      }
      this.$emit('submitForm', form)
      this.clearForm()
    },
    checkValid () {
      this.titleValid = !!this.title.length
      this.linkValid = !!this.link.length
      this.priceValid = !!this.realNumber
      if (this.titleValid && this.linkValid && this.priceValid) {
        this.allValid = true
      } else {
        this.allValid = false
      }
    }
  }
}
</script>

<style lang="scss">
.product-form {
  span {
    font-weight: 400;
    font-size: 10px;
  }
  padding-top: 32px;
    &__title {
        margin: 0;
        margin-bottom: 22px;
        font-size: 28px;
        color: #3F3F3F;
    }
    &__container {
        max-width: 332px;
        background: #FFFEFB;
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
        border-radius: 4px;
        padding: 24px;
        box-sizing: border-box;
    }
    &__form {
        text-align: left;
      label {
        margin-bottom: 8px;
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
    overflow: hidden;
    text-overflow: ellipsis;
    &::placeholder {
      color: #B4B4B4;
    }
    &:focus {
      border-color:#3F3F3F;
    }
  }
  &__input_invalid {
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
    margin-top: 17px;
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
  }

</style>
