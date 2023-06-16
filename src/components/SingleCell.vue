<template>
    <input type="text" class="cell" v-model="formula" @blur="calculate" @input="sendFormula" @focus="sendFormula">
</template>

<script>
    import { all, create } from 'mathjs';

    export default{
        data() {
            return {
                formula: '',
                value: ''
            }
        },
        methods: {
            calculate() {
                if(this.formula && this.formula.length > 0) {
                    if(this.formula.startsWith('=')) {
                        const math = create(all);

                        try {
                            this.value = math.evaluate(this.formula.substring(1));
                        } 
                        catch {
                            this.value = '#ERROR';
                        }
                    }
                }
            },
            sendFormula() {
                this.$emit('formulaSent', this.formula);
            }
        }
    }
</script>

<style>
    .cell{
        border: 1px solid #aaa;
        border-left: none;
        border-top: none;
        outline: none;
        padding: 0;
        width: 70px;
        height: 20px;
    }

</style>
