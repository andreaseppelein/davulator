<template>
  <div class="mx-auto overflow-hidden mt-10 shadow-lg mb-2 bg-purple-900 shadow-lg border rounded-lg lg:w-2/6 md:w-3/6 sm:w-4/6">
    <div class="">
      <div class="p-5 text-white text-center text-3xl bg-purple-900"><span class="text-orange-500">Dave</span>ulator</div>
      <div class="pt-16 p-5 pb-0 text-white text-right text-3xl bg-purple-800">{{ state.expression }}</div>
      <div class="p-5 text-white text-right text-3xl bg-purple-800"><span v-if="state.result.length > 0">=</span> <span class="text-orange-500">{{ state.result }}</span></div>


      <div class="flex items-stretch bg-purple-900 h-24">
        <CalculatorInputButton @addToExpression="addToExpression" type="placeholder" value=""></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="placeholder" value=""></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="placeholder" value=""></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="operator" value="division"></CalculatorInputButton>
      </div>

      <div class="flex items-stretch bg-purple-900 h-24">
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="7"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="8"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="9"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="operator" value="multiplication"></CalculatorInputButton>
      </div>

      <div class="flex items-stretch bg-purple-900 h-24">
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="4"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="5"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="6"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="operator" value="subtraction"></CalculatorInputButton>
      </div>

      <div class="flex items-stretch bg-purple-900 h-24">
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="1"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="2"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="3"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="operator" value="addition"></CalculatorInputButton>
      </div>


      <div class="flex items-stretch bg-purple-900 h-24 mb-4">
        <CalculatorInputButton type="action" value="reset" @click="resetCalculator"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="number" value="0"></CalculatorInputButton>
        <CalculatorInputButton @addToExpression="addToExpression" type="decimal" value="."></CalculatorInputButton>
        <CalculatorInputButton type="action" value="calculate" @click="calculateResult"></CalculatorInputButton>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">

import CalculatorInputButton from '@/components/CalculatorInputButton.vue';
import { reactive } from 'vue';

const state = reactive({
  expression: '',
  result: ''
})

function calculateResult() {
  state.result = eval(state.expression)
  state.expression = state.result
}

function addToExpression(char: string) {
  state.expression += char
}

function resetCalculator(): void {
  state.expression = ''
  state.result = ''
}
</script>
