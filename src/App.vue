<template>
  <div class="bg-emerald-100 min-h-screen">
   <h1 class="text-center p-4 pt-10 text-xl font-mono font-semibold">Calculadora</h1>
    <section class="flex flex-col mx-auto mt-10 p-2 md:w-2/6">

      <section>
        <input type="text" class="text-right w-full p-2 text-gray-400 bg-white" disabled v-model="topNumber">
        <input type="text" disabled v-model="initalValFormat" class="text-right p-3 bg-white text-2xl rounded shadow-sm w-full">
      </section>

      <section class="grid grid-cols-4 gap-1 mt-1 shadow-sm rounded-sm">
      <BtnComponent number="7" @click="addNumber(7)" />
      <BtnComponent number="8" @click="addNumber(8)"/>
      <BtnComponent number="9" @click="addNumber(9)"/>
      <BtnComponent number="X" @click="multiplicar"/>

      <BtnComponent number="4" @click="addNumber(4)"/>
      <BtnComponent number="5" @click="addNumber(5)"/>
      <BtnComponent number="6" @click="addNumber(6)"/>
      <BtnComponent number="-" @click="resta"/>

      <BtnComponent number="1" @click="addNumber(1)"/>
      <BtnComponent number="2" @click="addNumber(2)"/>
      <BtnComponent number="3" @click="addNumber(3)"/>
      <BtnComponent number="+" @click="suma"/>

      <BtnComponent number="0" @click="addNumber(0)"/>
      <BtnComponent number="." @click="addNumber('.')"/>
      <BtnComponent number="%" @click="dividir"/>
      <BtnComponent number="=" class="bg-blue-300" @click="resultado"/>

      <BtnComponent number="Clear" class="col-span-4 bg-green-300" @click="clearCalculator" />

      </section>

    </section>

  </div>
</template>

<script>
import BtnComponent from "./components/BtnComponent.vue";
import { reactive, ref } from '@vue/reactivity';
import { computed } from '@vue/runtime-core';
export default {
    components: { BtnComponent },
    setup(){

      const initialVal = ref('')
      const topNumber = ref(0)
      const operation = ref('')

      const numbers = reactive({firstnum : 0, secondNum : 0})

      const clearCalculator = () => {
        initialVal.value = ''
        numbers.firstnum = 0
        numbers.secondNum = 0
        topNumber.value = 0
      }

      const initalValFormat = computed(() => initialVal.value === '' ? 0 :initialVal.value)

      const setTopNumber = numb => topNumber.value = numb

      const checkNumbers = () => numbers.firstnum === 0 ? true : false

      const addNumber = num => initialVal.value = "" + initialVal.value + num

      const resultado = () =>  {
        switch (operation.value) {
          case '+':
            initialVal.value = parseFloat(numbers.firstnum) + parseFloat(initialVal.value)
            break;
          case '-':
            initialVal.value = parseFloat(numbers.firstnum) - parseFloat(initialVal.value)
            break;
          case 'x':
            initialVal.value = parseFloat(numbers.firstnum) * parseFloat(initialVal.value)
            break;
          case '/':
            initialVal.value = parseFloat(numbers.firstnum) / parseFloat(initialVal.value)
            break;
        }

        
        setTopNumber(0)
        numbers.firstnum = 0
        numbers.secondNum = 0

      }

      const suma = () => {
        const pos = checkNumbers()
        if ( pos ){
          operation.value = '+'
          numbers.firstnum = initialVal.value
          setTopNumber(`${initialVal.value} +`)
          initialVal.value = ''
        }else{
          numbers.secondNum = initialVal.value
          const total = parseFloat(numbers.firstnum) + parseFloat(numbers.secondNum)
          setTopNumber(0)
          initialVal.value = total
        }
      }

      const resta = () => {
        const pos = checkNumbers()
        if ( pos ){
          operation.value = '-'
          numbers.firstnum = initialVal.value
          setTopNumber(`${initialVal.value} -`)
          initialVal.value = ''
        }else{
          numbers.secondNum = initialVal.value
          const total = parseFloat(numbers.firstnum) - parseFloat(numbers.secondNum)
          setTopNumber(0)
          initialVal.value = total
        }
      }

      const multiplicar = () => {
        const pos = checkNumbers()
        if ( pos ){
          operation.value = 'x'
          numbers.firstnum = initialVal.value
          setTopNumber(`${initialVal.value} x`)
          initialVal.value = ''
        }else{
          numbers.secondNum = initialVal.value
          const total = parseFloat(numbers.firstnum) * parseFloat(numbers.secondNum)
          setTopNumber(0)
          initialVal.value = total
        }
      }

      const dividir = () => {
        const pos = checkNumbers()
        if ( pos ){
          operation.value = '/'
          numbers.firstnum = initialVal.value
          setTopNumber(`${initialVal.value} /`)
          initialVal.value = ''
        }else{
          numbers.secondNum = initialVal.value
          const total = parseFloat(numbers.firstnum) / parseFloat(numbers.secondNum)
          setTopNumber(0)
          initialVal.value = total
        }
      }



      return {
        initialVal,
        initalValFormat,
        topNumber,

        addNumber,
        clearCalculator,
        resultado,
        suma,
        resta,
        multiplicar,
        dividir,
      }

    }
}
</script>