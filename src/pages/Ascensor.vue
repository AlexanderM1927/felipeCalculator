<template>
  <q-page>
    <div class="row">
      <div class="col-2">
      </div>
      <div class="col-8">
        <div class="margen">
          <div class="ascensor">
            <div class="ascensor__display">{{ display }}</div>
            <div class="row">
              <div class="col-3 ascensor__button-container" v-for="index in 4" :key="index">
                <button class="ascensor__buton" :value="index" @click="cambiarDePiso(index)">{{ index }}</button>
              </div>
            </div>
            <div class="row">
              <div class="col-3"></div>
              <div class="col-6 ascensor__button-container">
                <button class="ascensor__buton" :value="5" @click="cambiarDePiso(5)">5</button>
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
      display: '1',
      pisoActual: 1
    }
  },
  setup () {
  },
  methods: {
    cambiarDePiso (piso) {
      // this.display = piso
      const _this = this
      const myInterval = setInterval(function () {
        if (_this.pisoActual < piso) {
          _this.pisoActual++
          _this.display = _this.pisoActual
        } else if (_this.pisoActual > piso) {
          _this.pisoActual--
          _this.display = _this.pisoActual
        } else {
          clearInterval(myInterval)
        }
      }, 2000)
    }
  }
})
</script>
<style lang="scss">
.margen {
  background: black;
  height: 100vh;
  width: 100%;
  position: relative;
}
.ascensor {
  background: white;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  width: 50%;
}
.ascensor__button-container {
  padding: 10px;
  display: flex;
  justify-content: center;
}
.ascensor__buton{
 border-radius: 50%;
  height: 50px;
  width: 50px;
  margin: 0;
  border: 0;
  font-weight: 500;
  font-size: 20px;
}
.ascensor__display{
  background: #FF0000;
  color: #FFF;
  padding: 10px;
  text-align: right;
  font-size: 40px;
  font-weight: 800;
  overflow-x: auto;
}
</style>
