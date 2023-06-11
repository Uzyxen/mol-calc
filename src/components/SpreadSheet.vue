<template>
  <div>
    <div id="columns">
      <div id="empty-space"></div>
      <div class="column" v-for="column in columns" :key="column">{{ column }}</div>
    </div>

    <div id="rows">
      <div class="row" v-for="row in 100" :key="row">{{ row }}</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return{
        columns: [
          'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
          'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'
        ]
      }
    }
  }
</script>

<style>
  #empty-space{
    width: 50px;
    background-color: #fff;
  }

  #columns{
    display: flex;
    position: sticky;
    top: 0;
  }

  #columns div:not(:nth-child(2)){
    border-left: none;
  }

  #rows div:not(:nth-child(1)){
    border-top: none;
  }

  .column{
    display: flex;
    justify-content: center;
    width: 70px;
    height: 20px;
    border: 1px solid #aaa;
  }

  .row{
    display: flex;
    justify-content: center;
    width: 49px;
    height: 20px;
    border: 1px solid #aaa;
    border-left: none;
  }
</style>
