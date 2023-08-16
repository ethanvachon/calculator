<template>
  <div class="container">
    <div class="row d-flex justify-content-center">
      <div class="col-auto">

        <div class="card d-flex flex-column m-5">
          <span class="secondary-screen text-muted">{{state.secondaryDisplay}} {{state.operator}}</span>  
          <div class="screen-padding">
            <input class="form-control screen" type="text" v-model="state.display">
          </div>
          <div class="d-flex button-area">
            <div class="col-3">
              <buttonTile @handleClick="clear()" :number="'C'" :color="'#a6a6a6'"></buttonTile>
              <buttonTile @handleClick="handleNum('7')" :number="'7'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('4')" :number="'4'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('1')" :number="'1'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('0')" class="width" :number="'0'" :color="'#505050'"></buttonTile>
            </div>
            <div class="col-3">
              <buttonTile :number="''" :color="'#a6a6a6'"></buttonTile>
              <buttonTile @handleClick="handleNum('8')" :number="'8'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('5')" :number="'5'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('2')" :number="'2'" :color="'#505050'"></buttonTile>
              <div></div>
            </div>
            <div class="col-3">
              <buttonTile :number="''" :color="'#a6a6a6'"></buttonTile>
              <buttonTile @handleClick="handleNum('9')" :number="'9'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('6')" :number="'6'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleNum('3')" :number="'3'" :color="'#505050'"></buttonTile>
              <buttonTile @handleClick="handleDecimal()" :number="'.'" :color="'#505050'"></buttonTile>
            </div>
            <div class="col-3">
              <buttonTile @handleClick="handleOperator('÷')" :number="'÷'" :color="'#ff8e00'"></buttonTile>
              <buttonTile @handleClick="handleOperator('x')" :number="'x'" :color="'#ff8e00'"></buttonTile>
              <buttonTile @handleClick="handleOperator('-')" :number="'-'" :color="'#ff8e00'"></buttonTile>
              <buttonTile @handleClick="handleOperator('+')" :number="'+'" :color="'#ff8e00'"></buttonTile>
              <buttonTile @handleClick="evaluate()" :number="'='" :color="'#ff8e00'"></buttonTile>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue'
import buttonTile from '@/components/button-tile.vue'

export default {
  name: 'App',
  components: {
    buttonTile,
  },
  setup() {
    const state = reactive({
      display: '',
      secondaryDisplay: '',
      operator: null,
    })
    return {
      state,
      handleNum: function (num) {
        state.display += num
      },
      clear: function () {
        state.display = ''
        state.secondaryDisplay = ''
        state.operator = null
      },
      handleOperator: function (operator) {
        if (state.operator == null) {
          state.secondaryDisplay = state.display
          state.display = ''
        }
        state.operator = operator
      },
      evaluate: function () {
        state.display = this.determineResult()
        state.secondaryDisplay = ''
        state.operator = null
      },
      determineResult: function () {
        switch(state.operator) {
          case ('÷'):
            return parseFloat(state.secondaryDisplay) / parseFloat(state.display)
          case ('x'):
            return parseFloat(state.secondaryDisplay) * parseFloat(state.display)
          case ('-'):
            return parseFloat(state.secondaryDisplay) - parseFloat(state.display)
          case ('+'):
            return parseFloat(state.secondaryDisplay) + parseFloat(state.display)
        }
      },
      handleDecimal: function () {
        if(!state.display.includes('.')) {
          state.display += '.'
        }
      },
    }
  },
}
</script>

<style scoped>
.screen {
  padding-bottom: 0px;
  font-size: 2em;
  font-weight: 500;
  padding-top: 0.5em;
}

.secondary-screen {
  position: relative;
    overflow: visible;
    height: 0px;
    width: 0px;
    top: 0.6em;
    left: 1.3em;
    white-space: nowrap;
}

.screen-padding {
  padding: 0.5em;
}

.card {
  background-color: black;
  padding: 0.75em;
  width: 21.5em;
}

.col-3 {
  display: flex;
  flex-direction: column;
}

.width {
  width: 200%;
}

.button-area {
  height: 25em;
}
</style>
