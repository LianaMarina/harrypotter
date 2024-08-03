<template>
  <div>
    <h4>Войти</h4>
<div class="Avto">
  <label for="#login">Логин</label>
  <input id="#login" type="text" v-model="user.login">
  <label for="#password">Пароль</label>
  <input id="#password" type="password" v-model="user.password">
</div>
    <button @click="avto">Войти</button>
</div>

</template>

<script>
export default {
  data() {
    return {
      user: {
        login: '',
        password: '',
      }
    }
  },
  methods: {
    avto() {
      this.$emit('avto', this.user);
      this.user.login = '';
      this.user.password = '';
    }
  }
}
</script>

<style scoped>
.Avto {
  display: flex;
  flex-direction: column;
}
label {
  padding-top: 10px;
}
h4 {
  text-align: center;
  font-size: 35px;
  font-weight: 600;
  padding-bottom: 15px;
}
button {
  border: 2px solid #000000;
  color: #000000;
  margin: 10px;
}

</style>