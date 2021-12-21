<template>
  <ul style="border-left: solid">
    <li v-for="item in selectedAmounts" v-bind:key="item">{{ item }}</li>
    <span>Выбрано: {{selectedAmounts}}</span>
  </ul>
</template>

<script>
export default {
  name: 'column3',
  data() {
    return {
      selectedAmounts: []
      //msg: ‘Welcome to Your Vue.js App’
  }
  }
}
</script>

<style scoped>

</style>