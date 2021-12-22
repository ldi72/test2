<template>
  <ul style="border-left: solid">
    <li v-for="item in displayData" v-bind:key="item.id">
      <input type="checkbox" v-bind:value="item.id" v-model="selectedAmountsChild">
      <label>{{ item }}</label>
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
  computed: {
    selectedAmountsChild: {
      get() {
        return this.selectedAmounts
      },
      set(selectedAmountsChild) {
        this.$emit('update:selectedAmounts', selectedAmountsChild)
      }
    },

    displayData() {
      if (this.isSorted) {return [...this.filterData].sort(function (a, b) {return a.amount-b.amount})}
      else {return [...this.filterData]}
    },

    filterData() {
      if (this.checkedItems === "2") {return this.rndData.filter(function(item) {return item.amount < 0})}
      else if (this.checkedItems === "3") {return this.rndData.filter(function(item) {return item.amount >= 0})}
      return this.rndData
    }

  }
}
</script>

<style scoped>

</style>