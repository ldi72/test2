<template>
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
      <input type="checkbox" v-bind:value="item.id" v-model="selectedAmounts">
      <label>{{ item }}</label><br>
    </li>
  </ul>

  <ul style="border-left: solid">
    <li v-for="item in selectedAmounts" v-bind:key="item">{{ item }}</li>
    <!--span>Выбрано: {{selectedAmounts}}</span-->
  </ul>
</template>

<script>
export default {
  name: 'App',
  created() {
    for ( let i = 0; i < 100; i++) {
      this.rndData.push({id: i+1, amount: Math.floor(Math.random() * (1000 - (-1000) + 1)) + (-1000)})
    }
  },
  data() {
    return {
      selectedAmounts: [],
      rndData: [],
      picked: '1',
      checked: false
    }
  },
  computed:
  {
    displayData()
    {
      let displayData = []
      if (this.picked == "1") {displayData = this.rndData}
      else if (this.picked == "2") {displayData = this.rndData.filter(item => item.amount < 0)}
      else if (this.picked == "3") {displayData = this.rndData.filter(item => item.amount >= 0)}

      if (this.checked) {displayData = displayData.sort(function (a, b) {return a.amount-b.amount})}
      else {displayData = displayData.sort(function (a, b) {return a.id-b.id})}

      return displayData
    }
    ,
    sortData()
    {
      let displayData = []
      if (this.checked) {displayData = this.rndData.sort(function (a, b) {return a.amount-b.amount})}
      else {displayData = this.rndData.sort(function (a, b) {return a.id-b.id})}
      return displayData
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