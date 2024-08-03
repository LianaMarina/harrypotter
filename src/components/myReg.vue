<template>
    <h4>Регистрация</h4>
    <div class="Reg">
    <label for="#login">Логин</label>
    <input id="#login" type="text" v-model="user.login">
    <label for="#password">Пароль</label>
    <input id="#password" type="password" v-model="user.password">
    <label for="#family">Фамилия</label>
    <input id="#family" type="text" v-model="user.family">
    <label for="#name">Имя</label>
    <input id="#name" type="text" v-model="user.name">
    <label for="#patronymic">Отчество</label>
    <input id="#patronymic" type="text" v-model="user.patronymic">
    <label for="#phone">Номер телефона</label>
    <input id="#phone" type="tel" v-model="user.phone">
    <label for="#gender">Пол</label>
    <input id="#gender" type="text" v-model="user.gender">
    <label for="#age">Возраст</label>
    <input id="#age" type="text" v-model="user.age">
      <strong style="padding-top: 20px">Выберите любимые факультеты:</strong>
      <div class="checbox">
    <div class="form-check">
      <input type="checkbox" id="#Griffindor" value="griffindor" v-model="user.facultet">
      <label for="#Griffindor">Гриффиндор</label>
    </div>
    <div class="form-check">
      <input type="checkbox" id="#Ravenclaw" value="ravenclaw" v-model="user.facultet">
      <label for="#Ravenclaw">Когтевран</label>
    </div>
    <div class="form-check">
      <input type="checkbox" id="#Hufflepuff" value="hufflepuff" v-model="user.facultet">
      <label for="#Hufflepuff">Пуффендуй</label>
    </div>
    <div class="form-check">
      <input type="checkbox" id="#Slytherin" value="slytherin" v-model="user.facultet">
      <label for="#Slytherin">Слизерин</label>
    </div>
      </div>
      <button @click="reg">Регистрация</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        login: '',
        password: '',
        family: '',
        name: '',
        patronymic: '',
        phone: '',
        gender: '',
        age: '',
        facultet: [],
      }
    }
  },
  methods: {
    reg() {
      this.$emit('reg', this.user);
      this.user.login = '';
      this.user.password = ''
      this.user.family = ''
      this.user.name =  ''
      this.user.patronymic =  ''
      this.user.phone = ''
      this.user.gender = ''
      this.user.age = ''
      this.user.facultet = []
    }
  }
}
</script>

<style scoped>
.Reg {
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
  margin-top: 10px;
}
.checbox {
  display: flex;
  justify-content: space-between;
  gap: 15px;
}
</style>