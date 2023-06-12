<template>
  <div id="container">
    <Spreadsheet/>
  </div>
</template>

<script>
import Spreadsheet from './components/SpreadSheet.vue'

export default {
  name: 'App',
  components: {
    Spreadsheet
  }
}
</script>

<style>
  #container{
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>
