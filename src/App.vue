<template>
  <div id="app">

    <column1  :is-sorted = "isSorted" @update:is-sorted ="isSorted = $event"
              :checked-items = "checkedItems" @update:checked-items = "checkedItems = $event"/>

    <column2  @update:selected-amounts="selectedAmounts = $event"
              :selected-amounts = "selectedAmounts"
              :is-sorted = "isSorted"
              :checked-items = "checkedItems"/>

    <column3  :selected-amounts = "selectedAmounts"/>

</div>
</template>

<script>
import column1 from "./components/column1";
import column2 from "./components/column2";
import column3 from "./components/column3";

export default {
  components: {
    column1,
    column2,
    column3
  },
  name: 'App',
  data() {
    return {
      selectedAmounts: [],
      checkedItems: '1',
      isSorted: false
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