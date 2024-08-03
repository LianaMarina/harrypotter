<template>
  <div>
    <select :value="modelValue" @change="filter1Change">
      <option selected value="none">Выберите параметр фильтрации</option>
      <slot></slot>
    </select>


  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
    },
    filters1: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    filter1Change($event) {
      this.$emit('update:modelValue', $event.target.value);
    },
  }
}
</script>

<style scoped>

</style>