<template>
  <transition name="slide-down">
    <div v-show="isShown" class="popup">
      <div class="popup-content">
        Товар успешно добавлен!
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'PopupSuccess',
  props: {
    isShown: {
      type: Boolean,
      default: true
    }
  }
}
</script>

<style lang="scss" scoped>
.popup {
    position: fixed;
    top: 50%;
    left: 50%;
    background: #7BAE73;
    color: #fff;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    &-content {
        padding: 10px 20px;
    }
}
.slide-down-enter-active, .slide-down-leave-active {
    opacity: 1;
}
.slide-down-enter, .slide-down-leave-to {
    opacity: 0;
}
</style>
