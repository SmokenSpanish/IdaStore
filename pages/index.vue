<template>
  <div class="main">
    <AppLayout>
      <ProductForm @submitForm="formSubmit" />
    </AppLayout>
  </div>
</template>

<script>
import AppLayout from '../layouts/AppLayout'
import ProductForm from '../components/ProductForm.vue'
export default {
  name: 'IndexPage',
  components: {
    AppLayout,
    ProductForm
  }
}
</script>

<style scoped lang="scss">

.main {
  background: rgba(255, 254, 251, 0.8);
  height: 100vh;
}
</style>
