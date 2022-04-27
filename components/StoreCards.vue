<template>
  <div class="card">
    <img class="card__image" :src="link" alt="image">
    <div class="card__body-wrapper">
      <h3 class="card__title">
        {{ title }}
      </h3>
      <p class="card__description">
        {{ description }}
      </p>
      <p class="card__price">
        {{ price }} руб.
      </p>
    </div>
    <button class="card__delete-btn" @click="handleDelete" />
  </div>
</template>

<script>
// import formattedPrice from '../filters/price-format'
export default {
  name: 'StoreCard',
  props: {
    id: {
      type: Number,
      required: true
    },
    title: {
      type: String,
      required: true
    },
    description: {
      type: String,
      default: ''
    },
    price: {
      type: String,
      required: true
    },
    link: {
      type: String,
      required: true
    }
  },
  methods: {
    handleDelete () {
      this.$emit('delete', this.id)
    }
  }
  // filter: {
  //   formattedPrice
  // }
}
</script>

<style lang="scss" scoped>
.card {
  position: relative;
  margin-left: 16px;
  border-radius: 4px;
  background-color: #FFFEFB;
  color: #3F3F3F;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  &__image {
    width: 100%;
    border-radius: 4px 4px 0 0;
  }
  &__body-wrapper {
    padding: 16px 16px 24px;
  }
  &__title {
    font-weight: 600;
    margin: 0;
    margin-bottom: 16px;
    font-weight: 20px;
  }
  &__description {
    font-size: 16px;
    margin-bottom: 32px;
  }
  &__price {
    font-weight: 600;
    font-size: 24px;
    margin: 0;
  }
  &__delete-btn {
    width: 32px;
    height: 32px;
    border-radius: 10px;
    background: url(/_nuxt/assets/images/delete.svg);
    border: none;
    background-position: center;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    position: absolute;
    top: -10px;
    right: -10px;
    cursor: pointer;
    transition: 0.3s;
  }
}
</style>
