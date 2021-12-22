<template>
  <ul>
    <input type="radio" id="one" value="1" v-model="pickedChild">
    <label for="one">Все</label>
    <br>
    <input type="radio" id="two" value="2" v-model="pickedChild">
    <label for="two">Меньше 0</label>
    <br>
    <input type="radio" id="three" value="3" v-model="pickedChild">
    <label for="three">Больше или равно 0</label>
    <br>
    <br>

    <input type="checkbox" id="checkbox" v-model="checkedChild">
    <label for="checkbox">Сортировка по дате</label>
  </ul>
</template>

<script>
export default {
  name: "column1",
  props: {
    isSorted: Boolean,
    checkedItems: String
  },
  computed: {
    checkedChild: {
      get() {
        return this.isSorted
      },
      set(checkedChild) {
        this.$emit('update:isSorted', checkedChild)
      }
    },
    pickedChild: {
      get() {
        return this.checkedItems
      },
      set(pickedChild) {
        this.$emit('update:checkedItems', pickedChild)
      }
    }
  }
}
</script>

<style scoped>

</style>