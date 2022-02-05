<template>
  <q-page>
    <div class="row">
      <div class="col-2">
      </div>
      <div class="col-8">
        <div class="calculator">
          <div class="calculator-children">
            <button value="0" @click="selectNumber">0</button>
            <button value="1" @click="selectNumber">1</button>
            <button value="2" @click="selectNumber">2</button>
            <button value="3" @click="selectNumber">3</button>
            <button value="1" @click="selectNumber">1</button>
            <button value="1" @click="selectNumber">1</button>
            <button value="1" @click="selectNumber">1</button>
            <button value="1" @click="selectNumber">1</button>
            <button @click="sum">+</button>
            <button @click="subtract">-</button>
            <button @click="operation">=</button>
            <div id="result">{{ resultado }}</div>
          </div>
        </div>
      </div>
      <div class="col-2">
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageIndex',
  data () {
    return {
      resultado: 0,
      operator: '+',
      yaDioClick: false
    }
  },
  setup () {
    const calculator = {
      numeroUno: [],
      numeroDos: []
    }
    return {
      calculator
    }
  },
  methods: {
    selectNumber (event) {
      const value = event.target.value
      if (!this.yaDioClick) {
        this.calculator.numeroUno.push(value)
      } else {
        this.calculator.numeroDos.push(value)
      }
    },
    sum () {
      this.yaDioClick = true
      this.operator = '+'
    },
    subtract () {
      this.yaDioClick = true
      this.operator = '-'
    },
    operation () {
      let numeroUno = ''
      for (let i = 0; i < this.calculator.numeroUno.length; i++) {
        numeroUno += this.calculator.numeroUno[i]
      }
      const numeroUnoInt = parseInt(numeroUno)
      let numeroDos = ''
      for (let i = 0; i < this.calculator.numeroDos.length; i++) {
        numeroDos += this.calculator.numeroDos[i]
      }
      const numeroDosInt = parseInt(numeroDos)
      if (this.operator === '+') {
        this.resultado = numeroUnoInt + numeroDosInt
      } else if (this.operator === '-') {
        this.resultado = numeroUnoInt - numeroDosInt
      }
      const nuevoNumero1 = []
      const result = this.resultado.toString()
      for (let i = 0; i < result.length; i++) {
        nuevoNumero1.push(result[i])
      }
      this.calculator.numeroUno = nuevoNumero1
      this.calculator.numeroDos = []
    }
  }
})
</script>
<style lang="scss">
.calculator {
  background: #D4AD0F;
  height: 100vh;
  width: 100%;
  position: relative;
}
.calculator-children {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  background: white;
  padding: 10px;
  border-radius: 10px;
}
</style>
