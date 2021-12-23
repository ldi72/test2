<template>
  <ul class="column">
    <li v-for="item in displayData" v-bind:key="item.id-1">
      <input type="checkbox" v-bind:value="item" v-model="selectedAmountsChild">
      <label>{{ item }}</label>
      <button v-on:click="item.amount++; this.rndData.splice(item.id-1,1,item)">+1</button>
      <button v-on:click="item.amount--">-1</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "column2",
  created() {
    for ( let i = 0; i < 100; i++) {
      this.rndData.push({id: i+1, amount: Math.floor(Math.random() * (1000 - (-1000) + 1)) + (-1000)})
    }
  },
  props: {
    checkedItems: String,
    isSorted: Boolean,
    selectedAmounts: Array
  },
  data() {
    return {
      rndData: []
    }
  },
  watch: {
    displayData() {
      console.log("displayData")
    },
    filterData() {
      console.log('filterData')
    }
  },
  computed: {
    selectedAmountsChild: {
      get() {
        return this.selectedAmounts
      },
      set(selectedAmountsChild) {
        this.$emit('update:selectedAmounts', selectedAmountsChild)
      },
    },

    displayData() {
      const displayData = [...this.filterData];
      if (this.isSorted) {displayData.sort(function (a, b) {return a.amount-b.amount})}
      return displayData
    },

    filterData() {
      let filterData = []
      if (this.checkedItems === "2") {filterData = this.rndData.filter(function(item) {return item.amount < 0})}
      else if (this.checkedItems === "3") {filterData = this.rndData.filter(function(item) {return item.amount >= 0})}
      filterData =  this.rndData
      return filterData
    }

  }
}
</script>

<style scoped>

</style>