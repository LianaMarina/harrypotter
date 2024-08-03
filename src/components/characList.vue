<template>
  <div>
  <charac-items
      v-for="charac in characters"
      :charac="charac"
      :key="charac.id"
      @openCard="$emit('openCard', charac)"
      :addFavVisible="addFavVisible"
      :deleteFavVisible="deleteFavVisible"
      @addFav="$emit('addFav', charac)"
      @deleteFav="$emit('deleteFav', charac)"
  />
  </div>
</template>

<script>
import characItems from "@/components/characItems";
export default {
  components: {characItems},
  props: {
    characters: {
      type: Array,
      required: true
    },
    addFavVisible: {
      type: Boolean,
      default: true,
    },
    deleteFavVisible: {
      type: Boolean,
      default: true,
    }
  }
}
</script>

<style scoped>

</style>