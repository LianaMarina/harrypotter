<template>
  <div>
    <div class="charac">
      <img v-if="charac.image!==''" :src="charac.image" class="portrait" alt="">
      <img v-else src="./img/no-photo.png" alt="" style="width: auto; padding-top: 50px; height: 300px">
      <div class="house">
        <img v-if="charac.house==='Gryffindor'" src="./img/gryffendor.png" alt="">
        <img v-if="charac.house==='Slytherin'" src="./img/слизерин.png" alt="">
        <img v-if="charac.house==='Hufflepuff'" src="./img/hufflepruff.png" alt="">
        <img v-if="charac.house==='Ravenclaw'" src="./img/ravenclaw.png" alt="">
      </div>
      <div class="info">
        <p class="name">{{charac.name}}</p>
        <p><span v-if="charac.dateOfBirth!==null">Дата рождения</span> {{charac.dateOfBirth}}</p>
        <p v-if="charac.house===''" class="facultet"><span>Факультет</span> -</p>
        <p><span>Актер</span> {{charac.actor}}</p>
        <p><span>Жив</span> {{charac.alive}}</p>
        <p v-if="charac.alternate_actors.length!==0"><span>Альтернативные актеры</span> {{charac.alternate_actors}}</p>
        <p v-if="charac.alternate_names.length!==0"><span>Альтернативные имена</span> {{charac.alternate_names}}</p>
        <p><span>Родословная</span> {{charac.ancestry}}</p>
        <p><span>Цвет глаз</span> {{charac.eyeColour}}</p>
        <p><span>Пол</span> {{charac.gender}}</p>
        <p><span>Работник Хогвартса</span> {{charac.hogwartsStaff}}</p>
        <p><span>Ученик Хогвартса</span> {{charac.hogwartsStudent}}</p>
        <p><span>Уникальный код</span> {{charac.id}}</p>
        <p><span>Патронус</span> {{charac.patronus}}</p>
        <p><span>Вид</span> {{charac.species}}</p>
        <p><span>Палочка</span> дерево: {{charac.wand.wood}}, сердцевина: {{charac.wand.core}}, длина: {{charac.wand.length}}</p>
        <p><span>Волшебник</span> {{charac.wizard}}</p>
        <p><span>Год рождения</span> {{charac.yearOfBirth}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    charac: {
      type: Object,
    }
  }
}
</script>

<style scoped>
.charac {
  padding: 10px;
  margin: 20px;
  display: flex;
  gap: 25px;
}
.portrait{
  height: 350px;
  width: auto;
  padding-top: 25px;
  border-radius: 15px;
}
.name {
  font-family: HarryPotter;
  font-size: 50px;
}
.birth span, .facultet {
  font-family: 'Caveat';
  font-size: 20px;
  font-weight: bolder;

}
p {
  font-family: 'Caveat';
  font-size: 25px;
  color: black;
}
.house img {
  width: 100px;
  height: auto;
  position: absolute;
  top: 15px;
  left: 15px;
}
</style>