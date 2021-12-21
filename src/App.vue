<template>
  <div id="app">
  <ul>
    <input type="radio" id="one" value="1" v-model="picked">
    <label for="one">Все</label>
    <br>
    <input type="radio" id="two" value="2" v-model="picked">
    <label for="two">Меньше 0</label>
    <br>
    <input type="radio" id="three" value="3" v-model="picked">
    <label for="three">Больше или равно 0</label>
    <br>
    <!--span>Выбрано: {{ picked }}</span-->
    <br>

    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">Сортировка по дате</label>
  </ul>

  <ul style="border-left: solid">
    <li v-for="item in displayData" v-bind:key="item.id">
      <input type="checkbox" v-bind:value="item.id" v-model="column3.data().selectedAmounts">
      <label>{{ item }}</label><br>
    </li>
  </ul>

  <column3/>
    <!--li v-for="item in selectedAmounts" v-bind:key="item">{{ item }}</li-->
    <!--span>Выбрано: {{selectedAmounts}}</span-->
  <!--/column3-->
</div>
</template>

<script>

import column3 from "./components/column3";

export default {
  components: {
    column3
  },
  name: 'App',
  created() {
    for ( let i = 0; i < 100; i++) {
      this.rndData.push({id: i+1, amount: Math.floor(Math.random() * (1000 - (-1000) + 1)) + (-1000)})
    }
  },
  data() {
    return {
      column3,
      //selectedAmounts: [],
      rndData: [],
      picked: '1',
      checked: false
    }
  },
  computed: {
    displayData()
    {
      let displayData = []
      if (this.checked) {displayData = [...this.filterData].sort(function (a, b) {return a.amount-b.amount})}
      else {displayData = [...this.filterData].sort(function (a, b) {return a.id-b.id})}

      return displayData
    }
    ,
    filterData()
    {
      let fData = []
      if (this.picked == "1") {fData = this.rndData}
      else if (this.picked == "2") {fData = this.rndData.filter(function(item) {return item.amount < 0})}
      else if (this.picked == "3") {fData = this.rndData.filter(function(item) {return item.amount >= 0})}
      return fData
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