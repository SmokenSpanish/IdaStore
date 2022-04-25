<template>
  <div class="main">
    <AppLayout>
      <ProductForm />
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
  background: #E5E5E5;
}
</style>
