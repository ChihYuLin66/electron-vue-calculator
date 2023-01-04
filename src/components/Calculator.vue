<script>
import { reactive, ref, watch} from 'vue'
export default {
  setup() {
    const display = ref(0);
    const operandA = ref('');
    const operator = ref('');
    const operandB = ref('');

    const isOperand = (n) => {
      return ['1', '2', '3', '4', '5', '6', '7', '8', '9', '0', '.'].includes(n);
    }
    const isOperator = (n) => {
      return ['+', '-', '*', '/'].includes(n);
    }
    const removeFirstZero = (n) => {
      return n.replace(/^0+/, '');
    }

    const show = (value) => {
      if (isOperand(value) === true) {
        display.value += value;
        display.value = removeFirstZero(display.value);
      }
    };

    // 計算
    const calc = () => {
      let formula = operandA + operator + operandB;

      display.value = eval(formula);
    };

    return {
      display,
      show
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="calc">
      <div class="display">{{ display }}</div>
      <div class="keypad">
        <div class="keys-row first-keys-row">
          <div class="key" @click="show('AC')">AC</div>
          <div class="key" @click="show('+/-')">+/-</div>
          <div class="key" @click="show('%')">%</div>
          <div class="key" @click="show('/')">/</div>
        </div>

        <div class="keys-row">
          <div class="key" @click="show('7')">7</div>
          <div class="key" @click="show('8')">8</div>
          <div class="key" @click="show('9')">9</div>
          <div class="key" @click="show('*')">*</div>
        </div>
        
        <div class="keys-row">
          <div class="key" @click="show('4')">4</div>
          <div class="key" @click="show('5')">5</div>
          <div class="key" @click="show('6')">6</div>
          <div class="key" @click="show('-')">-</div>
        </div>
        
        <div class="keys-row">
          <div class="key" @click="show('1')">1</div>
          <div class="key" @click="show('2')">2</div>
          <div class="key" @click="show('3')">3</div>
          <div class="key" @click="show('+')">+</div>
        </div>

        <div class="keys-row">
          <div class="key" @click="show('0')">0</div>
          <div class="key" @click="show('.')">.</div>
          <div class="key" @click="show('=')">=</div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
// source https://codepen.io/moeinmm/details/poZjyxv
/* Import Font */
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&display=swap");

/* GENERAL STYLES */
body {
    font-family: "Space Grotesk", sans-serif;

  direction: ltr;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #000;
}
.container {
  margin-top: 50px;
}

/* Calculator Styles */
.calc {
  color: #fff;
  width: 400px;
  padding: 15px;
}
.calc .display {
  padding: 15px;
  font-size: 3.2rem;
  margin-bottom: 20px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.keys-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
}
.keypad .keys-row .key {
  background-color: #333333;
  font-size: 2rem;
  text-align: center;
  width: 95px;
  line-height: 85px;
  border-radius: 50px;
  margin: 0 5px;
  cursor: pointer;
  user-select: none;
}
.keypad :first-child :nth-child(1),
.keypad :first-child :nth-child(2),
.keypad :first-child :nth-child(3) {
  background-color: #a5a5a5;
}
.keypad .keys-row .key:active {
  background-color: #a5a5a590;
}
.keypad .keys-row :last-child {
  background-color: #ffa45c;
}
.keypad .keys-row :last-child:active {
  background-color: #ffa45ccc;
}
.keypad :last-child :first-child {
  width: 190px;
}
</style>