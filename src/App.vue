<template>
  <ul>
    <input type="radio" id="one" value="1" v-model="picked" @change="RadioOnChange($event)" checked="checked">
    <label for="one">Все</label>
    <br>
    <input type="radio" id="two" value="2" v-model="picked" @change="RadioOnChange($event)">
    <label for="two">Меньше 0</label>
    <br>
    <input type="radio" id="three" value="3" v-model="picked" @change="RadioOnChange($event)">
    <label for="three">Больше или равно 0</label>
    <br>
    <!--span>Выбрано: {{ picked }}</span-->
    <br>

    <input type="checkbox" id="checkbox" @change="check($event)">
    <label for="checkbox">Сортировка по дате</label>
  </ul>

  <ul style="border-left: solid">
    <li v-for="item in displayData" v-bind:key="item.id">
      <input type="checkbox" v-bind:value="item.id" v-model="selectedAmounts">
      <label>{{item}}</label><br>
    </li>
  </ul>

  <ul style="border-left: solid">
    <li v-for="item in selectedAmounts"   v-bind:key="item">{{ item }}</li>
    <!--span>Выбрано: {{selectedAmounts}}</span-->
  </ul>

</template>

<script>
export default {
  name: 'App',
  data() {
    let rndData = [], displayData = [], selectedAmounts = []
    for (let i = 0; i < 100; i++){rndData.push({id: i+1, amount: Math.floor(Math.random() * (1000 - (-1000) + 1)) + (-1000)})}
    displayData = rndData;
    return{
      selectedAmounts,
      displayData,
      rndData,
      picked: ''
    }
  },
  methods: {
    check: function(e) {
      if (e.target.checked) {this.displayData = this.displayData.sort(function (a, b) {return a.amount-b.amount;})}
      else {this.displayData = this.displayData.sort(function (a, b) {return a.id-b.id;})}
    },
    RadioOnChange: function(e) {
      if (e.target.value == "1") {this.displayData = this.rndData.filter(function(number) {return number.amount;})}
      if (e.target.value == "2") {this.displayData = this.rndData.filter(function(number) {return number.amount < 0;})}
      if (e.target.value == "3") {this.displayData = this.rndData.filter(function(number) {return number.amount >= 0;})}
    }
  }
}
</script>

<style>
#app {
  display: flex;
}
</style>
<!-- justify-content: space-between;-->
<!--align-items: center;-->