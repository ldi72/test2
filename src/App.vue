<template>
  <div id="app">

    <column1  :is-sorted = "isSorted" @update:is-sorted ="isSorted = $event"
              :checked-items = "checkedItems" @update:checked-items = "checkedItems = $event"
              :sorted-direct = "sortedDirect" @update:sorted-direct = "sortedDirect = $event"
              :sorted-field = "sortedField" @update:sorted-field = "sortedField = $event"
    />

    <column2  @update:selected-amounts="selectedAmounts = $event"
              :selected-amounts = "selectedAmounts"
              :is-sorted = "isSorted"
              :checked-items = "checkedItems"
              :sorted-direct = "sortedDirect"
              :sorted-field = "sortedField"
    />

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
      isSorted: false,
      sortedDirect: 'forward',
      sortedField: 'id'
    }
  }
};

</script>

<style>
html, body, #app {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 100%;
}
#app {
  display: flex;
}
.column {
  border: 1px solid lightgray;
  overflow: hidden auto;
  min-width: 33%;

}
</style>
<!-- justify-content: space-between;-->
<!--align-items: center;-->