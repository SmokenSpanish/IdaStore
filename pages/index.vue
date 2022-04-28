<template>
  <div class="main">
    <app-layout>
      <product-form @submitForm="formSubmit" />
      <div class="store-wrapper">
        <on-count-filter style="margin-left: auto; margin-right: 22px" @filterChange="handleFilter" />
        <transition-group class="filter-wrapper" name="card" mode="out-in" tag="div">
          <div v-for="(item, index) in allProducts" :key="item.id" class="store-wrapper__item">
            <store-cards
              :id="item.id"
              :key="index"
              :title="item.title"
              :description="item.description"
              :link="item.link"
              :price="item.price"
              @delete="deleteItem"
            />
          </div>
        </transition-group>
      </div>
      <popup-success :is-shown="showSuccess" />
    </app-layout>
  </div>
</template>

<script>
import AppLayout from '../layouts/AppLayout'
import ProductForm from '../components/ProductForm.vue'
import StoreCards from '../components/StoreCards.vue'
import OnCountFilter from '~/components/OnCountFilter.vue'
import PopupSuccess from '~/components/PopupSuccess.vue'
export default {
  name: 'IndexPage',
  components: {
    AppLayout,
    ProductForm,
    StoreCards,
    OnCountFilter,
    PopupSuccess
  },
  data () {
    return {
      allProducts: [{
        id: 2345,
        title: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        price: '2 000',
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
    },
    handleFilter (value) {
      if (value === 'min') {
        this.allProducts.sort((a, b) => {
          return parseInt(a.price) - parseInt(b.price)
        })
      }
      if (value === 'max') {
        this.allProducts.sort((a, b) => {
          return parseInt(b.price) - parseInt(a.price)
        })
      }
      if (value === 'name') {
        this.allProducts.sort((a, b) => {
          return a.title < b.title ? -1 : 1
        })
      }
    }
  }
}
</script>

<style scoped lang="scss">

.main {
  background: rgba(255, 254, 251, 0.8);
  max-width: 1440px;
  height: 100vh;
  margin: 0 auto;
}
.store-wrapper {
  width: 74%;
  height: calc(100vh - 32px);
  overflow-y: scroll;
  scrollbar-width: none;
  padding-top: 32px;
  &::-webkit-scrollbar {
  display: none;
}
  &__item {
    width: 100%;
    max-width: 332px;
    margin: 0 0 16px 16px;
  }
}
.filter-wrapper {
  display: flex;
  flex-wrap: wrap;
  align-self: flex-start;
  width: 100%;
  margin-top: 16px;
}
.card-enter-active, .card-leave-active {
  transition: all 0.4s;
}
.card-enter, .card-leave-to {
  opacity: 0;
  transition: .5s;
  transform: opaticy .3s;
}
</style>
