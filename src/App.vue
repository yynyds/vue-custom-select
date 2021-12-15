<template>
  <div id="app">
    <CustomSelect
        v-model="myValueInCS"
        :items="itemsExample"
    />
  </div>
</template>

<script>

import CustomSelect from './components/CustomSelect'
export default {
  name: 'App',
  components: { CustomSelect },
  data: () => ({
    myValueInCS: null,
    itemsExample: [
      {
        "id": 1,
        "title": "delectus aut autem",
        "completed": false
      },
      {
        "id": 2,
        "title": "quis ut nam facilis et officia qui",
        "completed": false
      },
      {
        "id": 3,
        "title": "fugiat veniam minus",
        "completed": false
      },
      {
        "id": 4,
        "title": "et porro tempora",
        "completed": true
      }
    ]
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
