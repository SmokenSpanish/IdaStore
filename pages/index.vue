<template>
  <div class="main">
    <AppLayout>
      <ProductForm @submitForm="formSubmit" />
      <div class="store-wrapper">
        <div v-for="(item, index) in allProducts" :key="item.id" class="store-wrapper__item">
          <StoreCards
            :id="item.id"
            :key="index"
            :title="item.title"
            :description="item.description"
            :link="item.link"
            :price="item.price"
            @delete="deleteItem"
          />
        </div>
      </div>
    </AppLayout>
  </div>
</template>

<script>
import AppLayout from '../layouts/AppLayout'
import ProductForm from '../components/ProductForm.vue'
import StoreCards from '../components/StoreCards.vue'
export default {
  name: 'IndexPage',
  components: {
    AppLayout,
    ProductForm,
    StoreCards
  },
  data () {
    return {
      allProducts: [{
        id: 2345,
        title: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '2000',
        link: 'https://images.unsplash.com/photo-1646974708582-3dced57e0a25?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxlZGl0b3JpYWwtZmVlZHw3fHx8ZW58MHx8fHw%3D&auto=format&fit=crop&w=500&q=60'
      }],
      showSuccess: false,
      isProductsFetched: false
    }
  },
  mounted () {
    // const products = JSON.parse(window.localStorage.getItem('products'))
    // if (!products) {
    //   window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    // } else {
    //   this.allProducts = products
    // }
    // this.isProductsFetched = true
  },
  methods: {
    formSubmit (form) {
      this.allProducts.push(form)
      this.showSuccess = true
      setTimeout(() => {
        this.showSuccess = false
      }, 2000)
      window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    },
    deleteItem (id) {
      this.allProducts = this.allProducts.filter(item => item.id !== id)
      window.localStorage.setItem('products', JSON.stringify(this.allProducts))
    }
  }
}
</script>

<style scoped lang="scss">

.main {
  background: rgba(255, 254, 251, 0.8);
  height: 100vh;
}
.store-wrapper {
  margin-top: 16px;
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  align-items: stretch;
  &__item {
    flex: 0 0 calc(33% - 16px);
  }
}
</style>
