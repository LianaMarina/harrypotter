<template>
  <div>
    <div class="first-block" style="margin-top: 50px">
      <img src="./harryPotterWords.png" alt="">
      <h1>Добро пожаловать!</h1>
      <a href="#characters"><p class="top_p">Смотри персонажей ниже</p></a>
    </div>
<div style="min-height: 100vh">
    <div class="second_top">
        <div id="characters" class="regAndAvto">
          <!--НАЧАЛО РЕГИСТРАЦИИ-->
          <my-dialog v-model:show="regVisible">
            <my-reg @reg="regUser"/>
          </my-dialog>
          <button @click="openReg" style="border: 2px solid #ffae00; color: #ffae00; margin-right: 10px">Регистрация</button>
          <!--КОНЕЦ РЕГИСТРАЦИИ-->

          <!--НАЧАЛО АВТОРИЗАЦИИ-->
          <my-dialog v-model:show="avtoVisible">
            <my-avto @avto="avtoUser"/>
          </my-dialog>
          <button @click="openAvto" style="border: 2px solid #ffae00; color: #ffae00">Войти</button>
          <!-- КОНЕЦ АВТОРИЗАЦИИ     -->
        </div>
          <p style="color: white;padding: 10px 10px">{{familyName}}</p>

</div>
  <p style="position: relative; top: -15px; left: 40px" v-if="addFavVisible">Волшебники - {{countWizard}}  не волшебники {{countNoWizard}}</p>
      <div class="diffrentFunc" style="width: 100%;">
        <my-search v-model:value="searchValue"
                   @input="searchValue = $event.target.value"
        />
        <my-sort v-model="selectOption" :options="options"></my-sort>
        <my-filter v-model="selectFilter1" :filters1="filters1">
          <option v-for="filter1 in filters1"
          :key="filter1.id"
          :value="filter1.value">
                    {{filter1.name}}
                  </option>
        </my-filter>
        <my-filter v-model="selectFilter2" :filters2="filters2">
          <option v-for="filter2 in filters2"
                  :key="filter2.id"
                  :value="filter2.value">
            {{filter2.name}}
          </option>
        </my-filter>
      </div>

      <my-dialog v-model:show="dialogVisible" class="dialog">
        <my-card :charac="charac"/>
      </my-dialog>

      <charac-list
          class="list"
          v-bind:characters="searchList"
          @openCard="openCharac"
          :addFavVisible="addFavVisible"
          :deleteFavVisible="deleteFavVisible"
          @addFav="addFav"
          @deleteFav="deleteFav"
      />
    </div>
  </div>
</template>

<script>
import characList from "@/components/characList";
import MySearch from "@/components/mySearch";
import MySort from "@/components/mySort";
import MyFilter from "@/components/myFilter";
import MyDialog from "@/components/myDialog";
import MyReg from "@/components/myReg";
import MyCard from "@/components/myCard";
import MyAvto from "@/components/myAvto";
export default {
  components: {MyAvto, MyCard, MyReg, MyDialog, MyFilter, MySort, MySearch, characList},
  data() {
    return {
      characters: [],
      searchValue: '',
      selectOption: "none",
      selectFilter1: 'none',
      selectFilter2: 'none',
      options: [
        {value: 'name', name: 'Имя по возрастанию'},
        {value: 'name 1', name: 'Имя по убыванию'},
        {value: 'house', name: 'Факультет по возрастанию'},
        {value: 'house 1', name: 'Факультет по убыванию'},
        {value: 'actor', name: 'Актер по возрастанию'},
        {value: 'actor 1', name: 'Актер по убыванию'},
      ],
      filters1: [
        {id: '1', value: 'hogwartsStudent', name: 'Студенты Хогвартса'},
        {id: '2', value: 'hogwartsStaff', name: 'Работники Хогвартса'},
      ],
      filters2: [
        {id: '1', value: 'Gryffindor', name: 'Гриффиндор'},
        {id: '2', value: 'Slytherin', name: 'Слизерин'},
        {id: '3', value: 'Hufflepuff', name: 'Хуфлепуф'},
        {id: '4', value: 'Ravenclaw', name: 'Рэвенклоу'},
      ],
      dialogVisible: false,
      regVisible: false,
      avtoVisible: false,
      charac: {},
      familyName: '',
      addFavVisible: false,
      deleteFavVisible: false,
      favourite: [],
      countWizard: 0,
      countNoWizard: 0,
    }
  },
  methods: {
    async fetchCharacters() {
      let res = await fetch('https://hp-api.onrender.com/api/characters');
      this.characters = await res.json();
    },
    openCharac(charac) {
      this.charac = charac;
      this.dialogVisible = true;
    },
    openReg() {
      this.regVisible = true;
    },
    openAvto() {
      this.avtoVisible = true;
    },
    avtoUser(user) {
      let userAvto; //для хранения найденного пользователя
      for (let i = 0; i < localStorage.length; i++) {
        const key = localStorage.key(i); //получение ключа
        const value = localStorage[key]; //получение значения по ключу
        let userLocal = JSON.parse(value); //переводим в объект найденного пользователя
        if (userLocal.login === user.login && userLocal.password === user.password) {
          userAvto = user;
          this.addFavVisible = true;
          this.familyName = userLocal.family + ' ' + userLocal.name + ' ' + userLocal.patronymic;
          alert('Вход совершен успешно!')
        }
      }
      if (!userAvto) {
        alert('Неправильно введены логин или пароль');
      }
      this.avtoVisible = false;
    },
    regUser(user) {
      if (/^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{2,}$/.test(user.family)
          && /^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{2,}$/.test(user.patronymic)) {
        if (/^[АБВГДЕЁЖЗИЙКЛМНОПРСТУФХЦЧШЩЪЫЬЭЮЯ][абвгдеёжзийклмнопрстуфхцчшщъыьэюя]{1,}$/.test(user.name)) {
          if (/^8\([0-9]{3}\)[0-9]{3}-[0-9]{2}-[0-9]{2}$/.test(user.phone)) {
            if (/^(мужской|женский)$/.test(user.gender)) {
              if (user.age>10) {
                let key = Date.now();
                localStorage.setItem(key.toString(), JSON.stringify(user));
              } else {
                alert('Возраст должен быть больше 10')
              }
            } else {
              alert('Введите пол корректно')
            }
          } else {
            alert('Введите корректно номер телефона')
          }
        } else {
          alert('Введите корректно имя');
        }
      }
      else {
        alert('Введите корректно фамилию и отчество');
      }
      this.regVisible = false;
    },
    addFav(charac) {
      this.favourite.push(charac);
      if (charac.wizard) {
        this.countWizard++;
      } else {
        this.countNoWizard++;
      }
    },
    deleteFav(charac) {
      const index = this.favourite.indexOf(charac);
      if (charac.wizard) {
        this.countWizard--;
      } else {
        this.countNoWizard--;
      }
      this.favourite.splice(index, 1);
    }
  },
  computed: {
    searchList() {
      if (this.selectFilter1 !== 'none') {
        if (this.selectFilter2 !== 'none') {
          return [...this.filter2Charac].filter(charac => (charac.name.includes(this.searchValue))
              || (charac.house.includes(this.searchValue))
              || (charac.actor.includes(this.searchValue)));
        } else {
          return [...this.filter1Charac].filter(charac => (charac.name.includes(this.searchValue))
              || (charac.house.includes(this.searchValue))
              || (charac.actor.includes(this.searchValue)));
        }
      }
      if (this.selectFilter2 !== 'none') {
        if (this.selectFilter1 !== 'none') {
          return [...this.filter1Charac].filter(charac => (charac.name.includes(this.searchValue))
              || (charac.house.includes(this.searchValue))
              || (charac.actor.includes(this.searchValue)));
        } else {
          return [...this.filter2Charac].filter(charac => (charac.name.includes(this.searchValue))
              || (charac.house.includes(this.searchValue))
              || (charac.actor.includes(this.searchValue)));
        }
      } else {
        return [...this.sortList].filter(charac => (charac.name.includes(this.searchValue))
            || (charac.house.includes(this.searchValue))
            || (charac.actor.includes(this.searchValue)));
      }
    },
    // eslint-disable-next-line vue/return-in-computed-property
    sortList() {
      if (this.selectOption === "none") {
        return [...this.characters].filter(charac => (charac.name.includes(this.searchValue))
            || (charac.house.includes(this.searchValue))
            || (charac.actor.includes(this.searchValue)));
      } else {
        if ((this.selectOption.split(' ')).length === 1) {
            return [...this.characters].sort((p1, p2) => p1[(this.selectOption.split(' '))[0]]?.localeCompare(p2[(this.selectOption.split(' '))[0]]));
        } else if ((this.selectOption.split(' ')).length === 2) {
            return [...this.characters].sort((p1, p2) => p2[(this.selectOption.split(' '))[0]]?.localeCompare(p1[(this.selectOption.split(' '))[0]]));
        }
      }
    },
    filter1Charac() {
      if (this.selectFilter2 !== 'none') {
        if (this.selectOption !== 'none') {
          return [...this.sortList].filter(p => p[this.selectFilter1]);
        } else {
          return [...this.characters].filter(p => p[this.selectFilter1]);
        }
      } else {
        return [...this.sortList].filter(p => p[this.selectFilter1]);
      }
    },
    filter2Charac() {
      if (this.selectFilter1 !== 'none') {
        return [...this.filter1Charac].filter(p => p.house === this.selectFilter2);
      } else {
        return [...this.sortList].filter(p => p.house === this.selectFilter2);
      }
    },
    },
    mounted() {
      this.fetchCharacters();
    },
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;0,700;1,300;1,400;1,500;1,600;1,700&family=Jura:wght@300;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@400;500;600&family=Jura:wght@300;400;500;600;700&display=swap');
@font-face {
  font-family: 'HarryPotter';
  src: url("fonts/10467.ttf");
}

* {
  margin: 0 auto;
  scroll-behavior: smooth;
  box-sizing: border-box;
}
a {
  text-decoration: none;
}
.first-block {
  height: 100vh;
  text-align: center;
}
.first-block img {
  width: 300px;
}
h1 {
  padding-top: 125px;
  font-size: 100px;
}
h1, p {
  font-family: 'Cormorant Garamond';
  font-weight: 600;
  color: #ffae00;
}
.top_p {
  padding-top: 150px;
  font-size: 25px;
}
p.top_p::after {
  content: "";
  background: url("arrow.png") no-repeat;
  width: 50px;
  height: 50px;
  display: block;
  background-size: contain;
  margin: auto;
  transform: rotate(180deg);
}
.second_top {
  text-align: right;
  padding: 20px;
  font-family: 'Cormorant Garamond';
}
.second_top button {
  padding: 10px 15px;
  background: none;
  border-radius: 10px;
  font-family: 'Cormorant Garamond';
  font-weight: 600;
  font-size: 20px;
}
.list {
  text-align: center;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.diffrentFunc {
  display: flex;
  gap: 25px;
  flex-wrap: wrap;
}
input, select {
  padding: 5px 10px;
  border-radius: 5px;
}
.dialog {
  z-index: 1000;
}
select {
  background: none;
  color: #ffae00;
  border: 1px solid #ffae00;
  font-family: 'Cormorant Garamond';
  font-size: 18px;
}
select option {
  background: black;
}
input::placeholder {
  color: #ffae00;
}
</style>