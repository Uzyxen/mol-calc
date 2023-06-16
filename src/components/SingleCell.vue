<template>
    <input v-if="editMode" type="text" class="cell" 
    v-model="formula" 
    @blur="{ calculate(); editMode = false }" 
    @keyup.enter="{ calculate(); editMode = false }" 
    @input="sendFormula" 
    @focus="sendFormula"
    @vue:mounted="({ el }) => el.focus()">
    <span v-else class="cell" @click="editMode = true">{{ value }}</span>
</template>

<script>
    import { all, create } from 'mathjs';

    export default{
        data() {
            return {
                formula: '',
                value: '',
                editMode: false
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
        overflow: hidden;
    }

</style>
