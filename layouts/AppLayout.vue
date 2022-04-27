<template>
  <div class="container">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'AppLayout'
}
</script>

<style lang="scss" scoped>
.container {
    display: flex;
}
@media only screen and (max-width: 480px) {
.container {
    padding: 16px;
}
}
</style>
