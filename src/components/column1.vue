<template>
  <div class="column">
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

    <button v-on:click="direct('backward')">Назад</button>
    <button v-on:click="direct('forward')">Вперед</button>
    <br>
    <br>

    <select v-model="ChangeSelect">
      <option v-for="option in options" :value="option.idx" v-bind:key="option.idx">
         {{ option.text }}
      </option>
    </select>

  </div>
</template>

<script>
export default {
  name: "column1",
  props:
    ['checkedItems',
    'sortedDirect',
    'sortedField']
  ,
  created() {
    //this.selected = 2
    this.ChangeSelect = 2
  },
  data() {
    return {
      selected: 0,
      options: [
        { field: 'id', direct: 'forward', text: 'СортВперед по id', idx: 0 },
        { field: 'id', direct: 'backward', text: 'СортНазад по id', idx: 1 },
        { field: 'amount', direct: 'forward', text: 'СортВперед по amount', idx: 2 },
        { field: 'amount', direct: 'backward', text: 'СортНазад по amount ', idx: 3 }
      ]
    }
  },
  methods: {
    direct(direct) {
      if (direct === 'forward'){
        if (this.options.length-1 === this.ChangeSelect) this.ChangeSelect =0
        else this.ChangeSelect +=1}
      else {
        if (this.ChangeSelect === 0) this.ChangeSelect = this.options.length-1
        else this.ChangeSelect -=1}
    },
  },
  computed: {
    ChangeSelect:
    {
      get() {
        return this.selected
      },
      set(ChangeSelect){
        this.selected = ChangeSelect
        this.$emit('update:sortedField', this.options[ChangeSelect].field)
        this.$emit('update:sortedDirect', this.options[ChangeSelect].direct)
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