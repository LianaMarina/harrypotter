<template>
  <div>
    <label for="#search">Поиск</label>
    <input id="#search" :placeholder="searchValue" @input="$emit('update:searchValue', $event.target.value)">
  </div>
</template>

<script>
export default {
  props: {
    searchValue: {
      type: String,
      default: 'Найти',
    }
  },

}
</script>

<style scoped>
  label {
    color: #ffae00;
    padding-right: 15px;
    font-family: 'Cormorant Garamond';
    font-weight: 600;
  }
  input {
    background: none;
    color: #ffae00;
    border: 1px solid #ffae00;
    font-family: 'Cormorant Garamond';
    font-size: 18px;
  }
</style>