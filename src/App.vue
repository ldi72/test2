<template>
  <div id="app">
    <column1  v-model:checked-items = "checkedItems"
              v-model:sorted-direct = "sortedDirect"
              v-model:sorted-field = "sortedField"
    />
    <column2  v-model:selected-amounts = "selectedAmounts"
              v-model:checked-items = "checkedItems"
              v-model:sorted-direct = "sortedDirect"
              v-model:sorted-field = "sortedField"
    />
    <column3  v-model:selected-amounts = "selectedAmounts"/>
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
      sortedDirect: 'forward',
      sortedField: 'id',
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