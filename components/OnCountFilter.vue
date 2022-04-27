<template>
  <select id="price" class="select" name="price" @change="filterChange($event)">
    <option value="default" selected>
      По умолчанию
    </option>
    <option value="min">
      По нарастающей
    </option>
    <option value="max">
      По убыванию
    </option>
    <option value="name">
      По наименованию
    </option>
  </select>
</template>

<script>
export default {
  name: 'ProductFilter',
  methods: {
    filterChange (event) {
      this.$emit('filterChange', event.target.value)
    }
  }
}
</script>

<style lang="scss" scoped>
.select {
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
</style>
