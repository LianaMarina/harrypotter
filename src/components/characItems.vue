<template>
  <div class="charac" @click="$emit('openCard', charac)">
    <img v-if="charac.image!==''" :src="charac.image" class="portrait" alt="">
    <img v-else src="./img/no-photo.png" alt="" style="width: 150px; padding-top: 50px">
    <div class="name">{{charac.name}}</div>
    <div class="birth"><span v-if="charac.dateOfBirth!==null">Дата рождения</span> {{charac.dateOfBirth}}</div>
    <div v-if="charac.house===''" class="facultet"><span>Факультет</span> -</div>
    <div class="house">
      <img v-if="charac.house==='Gryffindor'" src="./img/gryffendor.png" alt="">
      <img v-if="charac.house==='Slytherin'" src="./img/слизерин.png" alt="">
      <img v-if="charac.house==='Hufflepuff'" src="./img/hufflepruff.png" alt="">
      <img v-if="charac.house==='Ravenclaw'" src="./img/ravenclaw.png" alt="">
    </div>
    <div>
      <button v-if="addFavVisible1&&addFavVisible" @click.stop @click="addFav" class="addFav">Добавить в избранное</button>
      <button v-if="deleteFavVisible1" @click.stop @click="deleteFav"  class="deleteFav">Удалить из избранного</button>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    charac: {
      type: Object,
      required: true,
    },
    addFavVisible: {
      type:Boolean,
    }
  },
data() {
    return {
      addFavVisible1: true,
      deleteFavVisible1: false,
    }
},
  methods: {
    addFav() {
      this.$emit('addFav', this.charac);
      this.addFavVisible1 = false;
      this.deleteFavVisible1 = true;
    },
    deleteFav() {
      this.$emit('deleteFav', this.charac);
      this.addFavVisible1 = true;
      this.deleteFavVisible1 = false;
    }
  }
}
</script>

<style scoped>
  .charac {
    min-width: 150px;
    width: 300px;
    padding: 10px;
    margin: 20px;
    background-image: url("img/pngwing.com.png");
    background-repeat: no-repeat;
    background-size: cover;
    position: relative;
    cursor: pointer;
  }
  .portrait{
    height: 250px;
    width: auto;
    padding-top: 50px;
    border-radius: 15px;
  }
  .name {
    font-family: HarryPotter;
    font-size: 35px;
  }
  .birth span, .facultet {
    font-family: 'Caveat';
    font-size: 20px;
    font-weight: bolder;

  }
  .birth {
    font-family: 'Caveat';
    font-size: 20px;
  }
.house img {
  width: 100px;
  height: auto;
  position: absolute;
  top: 15px;
  left: 25px;
}
button {
  padding: 10px 20px;
  border-radius: 10px;
  border: none;
  color: white;
  cursor: pointer;
  font-family: 'Caveat';
  font-size: 20px;
}

  .addFav {
    background: #008b5a;
  }
.addFav:hover {
  background: #006e49;
  transition: 0.1s;
}
  .deleteFav {
    background: darkred;
  }
  .deleteFav:hover {
    background: #720101;
    transition: 0.1s;
  }
</style>