<script>
import { getCurrentInstance } from 'vue';
import ButtonCalc from './ButtonCalc.vue';

export default {
    name: 'Calculatrice',
    props: {
        msg: String
    },
    components: {
        ButtonCalc
    },

    data() {
        return {
            calcVal: '',
            calcBtns: ['C', '%', '=', '+', 7, 8, 9, '-', 4, 5, 6, '*', 1, 2, 3, '/', 0, '.'],
            operators: null,
            prevCalcVal: ''
        }
    },
    
    methods: {
        isOperator(btn) {
            return ['C', '*', '/', '+', '-', '=', '%'].includes(btn);
        },
        showHistory(){
            console.log("pour afficher l'historique plus tard");
        },
        action(btn) {

            if (!isNaN(btn) || btn === '.') {
                this.calcVal += btn + ''
            }

            if (btn === 'C') {
                this.calcVal = ''
            }

            if (btn === '%') {
                this.calcVal = this.calcVal / 100 + ''
            }

            if (['/', '+', '-', '*'].includes(btn)) {
                this.operators = btn
                this.prevCalcVal = this.calcVal
                this.calcVal = ''
            }

            if (btn === "=") {
                this.calcVal = eval(
                    this.prevCalcVal + this.operators + this.calcVal
                )
                this.prevCalcVal = ''
                this.operators = null
            }
        }
    },
}
</script>



<template>
    <div class=containerHistory>
        <button type="button" @click="showHistory">Click</button>
    </div>
    <div class="calculatorBox">
        <div class="resultCalcul">
            {{ calcVal || 0 }}
        </div>

        <div class="allButtonsCalc">
            <ButtonCalc v-for="btn in calcBtns" :key="btn" :button-text="btn" :is-operator="isOperator(btn)" @button-click="action"></ButtonCalc>
        </div>
    </div>
</template>

<style scoped>
.calculatorBox {
    max-width: 400px;
    margin: 50px auto;
    background-color: rgb(43, 68, 34);
    padding: 1.5rem;
}

.resultCalcul {
    border-radius: 0.25rem;
    margin-bottom: 0.5rem;
    padding: 0.75rem;
    text-align: right;
    font-weight: bold;
    color: #fff;
    background-color: #315e3c;
}

.allButtonsCalc {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
}


</style>
