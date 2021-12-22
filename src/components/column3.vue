<template>
  <ul style="border-left: solid">
    <li v-for="item in selectedAmounts" v-bind:key="item">
      id: {{ item.id }}, amount: {{ item.amount }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'column3',
  props: {
    selectedAmounts: Array
  }
}
</script>

<style scoped>

</style>