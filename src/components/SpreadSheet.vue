<template>
  <div>
    <div id="topbar">

    </div>

    <FormulaInput :formula="formula" :focusedCell="focusedCell"/>

    <div id="main">
      <div id="columns">
        <div id="empty-space"></div>
        <div class="column" v-for="column in columns" :id="column" :key="column" :class="{ 'focused': column === focusedColumn}">{{ column }}</div>
      </div>

      <div id="rows">
        <div class="row" v-for="row in 30" :id="row" :key="row" :class="{ 'focused': row === focusedRow}">{{ row }}</div>
      </div>

      <div id="sheet">
        <div class="sheet-row" v-for="row in 30" :key="row">
          <SingleCell :id="column + row" @click="focusedCell = column + row" v-for="column in columns" :key="column" @formulaSent="handleEvent"/>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import FormulaInput from './FormulaInput.vue';
  import SingleCell from './SingleCell.vue';

  export default {
    data() {
      return{
        columns: [
          'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
          'N', 'O'
        ],
        focusedColumn: '',
        focusedRow: '',
        focusedCell: '',
        formula: ''
      }
    },

    methods:{
      handleEvent(value) {
        this.formula = value;
      },

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

      evaluateCellReferences(expression) {
        const cellReferenceRegex = /[A-Z]+\d+/g;
        const cellReferences = expression.match(cellReferenceRegex);

        if (cellReferences) {
          for (const cellRef of cellReferences) {
            const cellValue = this.inputValues[cellRef];
            expression = expression.replace(cellRef, cellValue);
          }
        }

        return expression;
      }
    },
    components: {
      SingleCell,
      FormulaInput
    }
  }
</script>

<style>
  #topbar{
    height: 70px;
    border-bottom: 1px solid #ddd;
  }

  #main{
    position: relative;
  }

  #empty-space{
    width: 50px;
    height: 20px;
    background-color: #fff;
    border-top: 1px solid #aaa;
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
    height: 21px;
    border: 1px solid #aaa;
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
    top: 23px;
    left: 51px;
    width: calc(100% - 50px);
    height: 250vh;
  }

  .sheet-row{
    display: flex;
    width: 300vh;
    height: 21px;
  }

  .sheet-column.focused{
    z-index: 99;
    border: 2px solid #000;
    height: 17px;
    width: 67px;
  }
</style>
