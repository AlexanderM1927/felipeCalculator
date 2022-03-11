<template>
  <q-page>
    <div class="row">
      <div class="col-2">
      </div>
      <div class="col-8">
        <div class="calculator">
          <div class="calculator-children">
            <div class="calculator-children__history">{{ historial }}</div>
            <div class="calculator-children__result">{{ resultado }}</div>
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
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton" @click="multiplier">*</button>
              </div>
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton button-primary" @click="igual">=</button>
              </div>
              <div class="col-4 calculator-children__button-container">
                <button class="calculator-children__buton" @click="divisor">/</button>
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
      yaDioClick: false,
      historial: '',
      yaHizoOperacion: false
    }
  },
  setup () {
    const calculator = {
      numeroUno: [],
      numeroDos: [],
      numeroTres: []
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
    saveHistorial (operation) {
      this.historial += this.passArrayNumToIntNum(this.calculator.numeroUno) + operation
    },
    actAsIgual () {
      if (this.calculator.numeroDos.length === 0) this.calculator.numeroDos = ['0']
      console.log('inicio con', this.passArrayNumToIntNum(this.calculator.numeroTres))
      if (this.yaHizoOperacion) {
        if (this.operator === '+') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroTres) + this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '-') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroTres) - this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '*') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroTres) * this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '/') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroTres) / this.passArrayNumToIntNum(this.calculator.numeroDos)
        }
      } else {
        if (this.operator === '+') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) + this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '-') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) - this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '*') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) * this.passArrayNumToIntNum(this.calculator.numeroDos)
        } else if (this.operator === '/') {
          this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) / this.passArrayNumToIntNum(this.calculator.numeroDos)
        }
      }
      const resultInArray = []
      const result = this.resultado.toString()
      for (let i = 0; i < result.length; i++) {
        resultInArray.push(result[i])
      }
      this.calculator.numeroTres = resultInArray
      this.calculator.numeroDos = []
      console.log('termino con', this.passArrayNumToIntNum(this.calculator.numeroTres))
      this.yaHizoOperacion = true
    },
    sum () {
      this.saveHistorial('+')
      this.yaDioClick = true
      this.operator = '+'
      this.resultado += this.operator
      this.actAsIgual()
    },
    subtract () {
      this.saveHistorial('-')
      this.yaDioClick = true
      this.operator = '-'
      this.resultado += this.operator
      this.actAsIgual()
    },
    multiplier () {
      this.saveHistorial('*')
      this.yaDioClick = true
      this.operator = '*'
      this.resultado += this.operator
      this.actAsIgual()
    },
    divisor () {
      this.saveHistorial('/')
      this.yaDioClick = true
      this.operator = '/'
      this.resultado += this.operator
      this.actAsIgual()
    },
    igual () {
      if (this.operator === '+') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) + this.passArrayNumToIntNum(this.calculator.numeroDos)
      } else if (this.operator === '-') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) - this.passArrayNumToIntNum(this.calculator.numeroDos)
      } else if (this.operator === '*') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) * this.passArrayNumToIntNum(this.calculator.numeroDos)
      } else if (this.operator === '/') {
        this.resultado = this.passArrayNumToIntNum(this.calculator.numeroUno) / this.passArrayNumToIntNum(this.calculator.numeroDos)
      }
      const resultInArray = []
      const result = this.resultado.toString()
      for (let i = 0; i < result.length; i++) {
        resultInArray.push(result[i])
      }
      this.calculator.numeroUno = resultInArray
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
  width: 50%;
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
  overflow-x: auto;
}
.calculator-children__history {
  background: #E74C3C;
  color: #FFF;
  padding: 10px;
  text-align: right;
  font-size: 20px;
  font-weight: 800;
  border-radius: 10px 10px 0px 0px;
  overflow-x: auto;
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
