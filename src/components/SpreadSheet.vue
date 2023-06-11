<template>
  <div>
    <div id="columns">
      <div id="empty-space"></div>
      <div class="column" v-for="column in columns" :key="column">{{ column }}</div>
    </div>

    <div id="rows">
      <div class="row" v-for="row in 100" :key="row">{{ row }}</div>
    </div>

    <div id="sheet">
      <div class="sheet-row" v-for="row in 100" :key="row">
        <input type="text" class="sheet-column" v-for="column in columns" :key="column" :id="column + row" v-model="inputValues[column + row]">
      </div>
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
        ],

        inputValues: {}
      }
    },

    methods:{

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
    width: 300vh;
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
    border-top: none;
  }

  .row{
    display: flex;
    justify-content: center;
    width: 50px;
    height: 20px;
    border: 1px solid #aaa;
    border-left: none;
  }

  #sheet{
    position: absolute;
    top: 22px;
    left: 51px;
    width: calc(100% - 50px);
    height: 250vh;
  }

  .sheet-row{
    display: flex;
    width: 100%;
    height: 21px;
  }

  .sheet-column{
    border: 1px solid #aaa;
    border-left: none;
    border-top: none;
    outline: none;
    padding: 0;
    width: 70px;
    height: 20px;
  }
</style>
