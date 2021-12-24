<template>
  <ul class="column">
    <li v-for="item in SortedFilteredData" v-bind:key="item.id">
      <input type="checkbox" v-bind:value="item" v-model="selectedAmountsChild">
      <label>{{ item }}</label>
      <button v-on:click="item.amount +=1; this.rndData.splice(item.id-1,1,item)">+1</button>
      <button v-on:click="item.amount -=1">-1</button>
    </li>
  </ul>
</template>

<script>
  const compareBy = (key) => (a, b) => a[key] - b[key]

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
    selectedAmounts: Array,
    sortedDirect: String,
    sortedField: String
  },
  data() {
    return {
      rndData: []
    }
  },
  /*watch: {
    SortedFilteredData: {
      handler(){ console.log("SortedFilteredData")}, deep: true
    },
    FilteredData: {
      handler(){ console.log("FilteredData")}, deep: true
    },
  },*/
  computed: {
    selectedAmountsChild: {
      get() {
        return this.selectedAmounts
      },
      set(selectedAmountsChild) {
        this.$emit('update:selectedAmounts', selectedAmountsChild)
      },
    },

    SortedFilteredData() {
      //const SortedFilteredData = [...this.FilteredData];
      //if (this.isSorted) {SortedFilteredData.sort(compareBy('amount'))}
      const SortedFilteredData = [...this.FilteredData].sort(compareBy(this.sortedField))
      if (this.sortedDirect === 'backward') SortedFilteredData.reverse()
      return SortedFilteredData
    },

    FilteredData() {
      if (this.checkedItems === "2") {return this.rndData.filter(function(item) {return item.amount < 0})}
      else if (this.checkedItems === "3") {return this.rndData.filter(function(item) {return item.amount >= 0})}
      return this.rndData
    }

  }
}
</script>

<style scoped>

</style>