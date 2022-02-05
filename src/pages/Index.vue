<template>
  <q-page>
    <div class="row">
      <div class="col-2">
      </div>
      <div class="col-8">
        <div class="calculator">
          <div class="calculator-children">
            <div id="result" class="calculator-children__result">{{ resultado }}</div>
            <div class="row">
              <div class="col-4 calculator-children__button-container" v-for="index in 9" :key="index">
                <button class="calculator-children__buton" :value="index" @click="selectNumber">{{ index }}</button>
              </div>
            </div>
            <div class="row">
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton" @click="sum">+</button>
              </div>
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton" value="0" @click="selectNumber">0</button>
              </div>
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton" @click="subtract">-</button>
              </div>
            </div>
            <div class="row">
              <div class="col-12 calculator-children__button-container">
                <button class="calculator-children__buton button-primary" @click="operation">=</button>
              </div>
            </div>
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
    passArrayNumToIntNum (array) {
      let numeroUno = ''
      for (let i = 0; i < array.length; i++) {
        numeroUno += array[i]
      }
      return parseInt(numeroUno)
    },
    selectNumber (event) {
      const value = event.target.value
      if (!this.yaDioClick) {
        this.calculator.numeroUno.push(value)
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno)
      } else {
        this.calculator.numeroDos.push(value)
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroDos)
      }
    },
    sum () {
      this.yaDioClick = true
      this.operator = '+'
      this.resultado += this.operator
    },
    subtract () {
      this.yaDioClick = true
      this.operator = '-'
      this.resultado += this.operator
    },
    operation () {
      if (this.operator === '+') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) + this.passArrayNumToIntNum(this.calculator.numeroDos)
      } else if (this.operator === '-') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) - this.passArrayNumToIntNum(this.calculator.numeroDos)
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
  background: black;
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
  border-radius: 10px;
}
.calculator-children__buton {
  border-radius: 50%;
  height: 50px;
  width: 50px;
  margin: 0;
  border: 0;
  font-weight: 500;
  font-size: 20px;
}
.calculator-children__result {
  background: #FF0000;
  color: #FFF;
  padding: 10px;
  text-align: right;
  font-size: 40px;
  font-weight: 800;
  border-radius: 10px 10px 0px 0px;
}
.calculator-children__button-container {
  display: flex;
  justify-content: center;
  padding: 10px;
}
.button-primary {
  background: #FF0000;
  color: #FFFFFF;
}
</style>
