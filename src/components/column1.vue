<template>
  <ul class="column">
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
    <br>
    <br>

    <button v-on:click="direct('forward')">Вперед</button>
    <button v-on:click="direct('backward')">Назад</button>

  </ul>
</template>

<script>
export default {
  name: "column1",
  props: {
    isSorted: Boolean,
    checkedItems: String,
    sortedDirect: String,
    sortedField: String
  },
  data() {
    return {
      //sortedDirectChild: 'forward',
      //sortedFieldChild: 'id'
    }
  },
  methods: {
    direct(direct) {
      if (this.sortedField === 'id') {this.$emit('update:sortedField', 'amount')}
      else {this.$emit('update:sortedField', 'id')}
      this.$emit('update:sortedDirect', direct)
    },
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