<template>
  <div>
    <div id="functions">
      <h2>=</h2>
      <input type="text" id="formula" v-model="focusedCellValue" @input="inputValues[focusedCell] = focusedCellValue" @keyup.enter="calculate(focusedCell)">
    </div>


    <div id="main">
      <div id="columns">
        <div id="empty-space"></div>
        <div class="column" v-for="column in columns" :id="column" :key="column" :class="{ 'focused': column === focusedColumn}">{{ column }}</div>
      </div>

      <div id="rows">
        <div class="row" v-for="row in 100" :id="row" :key="row" :class="{ 'focused': row === focusedRow}">{{ row }}</div>
      </div>

      <div id="sheet">
        <div class="sheet-row" v-for="row in 100" :key="row">
          <input type="text" class="sheet-column" v-for="column in columns" :key="column"
          :id="column + row" 
          v-model="inputValues[column + row]" 
          @focus="inputFocused(column, row)"
          @blur="{ inputBlur; calculate(column + row); }"
          @input="focusedCellValue = inputValues[column + row]"
          :class="{ 'focused': column + row === focusedCell}">
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import { all, create } from 'mathjs'

  export default {
    data() {
      return{
        columns: [
          'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
          'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'
        ],
        focusedColumn: '',
        focusedRow: '',
        focusedCell: '',
        focusedCellValue: 0,

        inputValues: {}
      }
    },

    methods:{
      inputFocused(column, row) {
        this.focusedColumn = column;
        this.focusedRow = row;
        this.focusedCell = column + row;
        this.focusedCellValue = this.inputValues[this.focusedCell];
      },

      inputBlur() {
        this.focusedColumn = '';
        this.focusedRow = '';
        this.focusedCell = '';
      },


      calculate(id){
        const value = this.inputValues[id];

        if(value && value.length > 0){
          if(value.startsWith('=')){
              const math = create(all);

              try{
                this.inputValues[id] = math.evaluate(value.substring(1));
              } catch (error){
                this.inputValues[id] = "#ERROR";
              }

              //this.inputValues[id] = this.inputValues[value.substring(1)];
          }
        }
      }
    }
  }
</script>

<style>
  #functions{
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }

  #functions h2{
    margin: 0;
  }

  #formula{
    outline: none;
    border: 1px solid #aaa;
    height: 20px;
    position: relative;
  }

  #main{
    position: relative;
  }

  #empty-space{
    width: 50px;
    background-color: #fff;
  }

  #columns{
    display: flex;
    position: sticky;
    top: 0;
    width: 300vh;
    z-index: 99;
    background-color: #fff;
  }

  #rows{
    z-index: 99;
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

  .column.focused{
    background-color: blue;
    border-color: blue;
    color: #fff;
  }

  .row{
    display: flex;
    justify-content: center;
    width: 50px;
    height: 20px;
    border: 1px solid #aaa;
    border-left: none;
  }

  .row.focused{
    background-color: red;
    border-color: red;
    color: #fff;
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

  .sheet-column.focused{
    z-index: 99;
    border: 2px solid #000;
    height: 17px;
    width: 67px;
  }
</style>
