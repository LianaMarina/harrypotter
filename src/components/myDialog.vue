<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div class="dialogContent" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideDialog() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style scoped>
span {
  font-weight: bolder;
  color: darkred;
}
.dialog {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
}
.dialogContent {
  margin: auto;
  position: relative;
  /*background-image: url("pngwing.com.png");*/
  background-repeat: no-repeat;
  background-size: contain;
  background-color: rgb(255, 210, 125);
  border-radius: 10px;
  /*border: 2px solid rgba(255, 255, 255, 0.25);*/
  padding: 20px;
  min-width: 300px;
}


</style>