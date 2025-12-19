<template>
    <h1>Math Quiz App</h1>
    <OperatorSelector v-if="!operator" @changeOperator="changeOperator" />
    <OperatorQuiz @onBack="clearOperator" v-if="operator" :operator="operator" />
</template>

<script>
import OperatorSelector from './components/OperatorSelector.vue';
import OperatorQuiz from './components/OperatorQuiz.vue';

export default {
    name: 'app',
    data() {
        return {
            operator: null
        }
    },
    methods: {
        changeOperator(operator) {
            this.operator = operator;
        },
        clearOperator() {
            this.operator = null;
        }
    },
    components: { OperatorSelector, OperatorQuiz }
};
</script>

<style>
#app {
    font-family: "Avenir", Arial, Helvetica, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

button {
    padding: 10px;
    width: 160px;
    height: 80px;
    margin-right: 10px;
    background-color: #10eab2;
    color: white;
    font-size: 24px;
    cursor: pointer;
    vertical-align: top;
}
</style>
