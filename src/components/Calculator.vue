<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="button">C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percentage" class="button">%</div>
    <div @click="divide" class="button operator">÷</div>
    <div @click="append('7')" class="button">7</div>
    <div @click="append('8')" class="button">8</div>
    <div @click="append('9')" class="button">9</div>
    <div @click="multiply" class="button operator">x</div>
    <div @click="append('4')" class="button">4</div>
    <div @click="append('5')" class="button">5</div>
    <div @click="append('6')" class="button">6</div>
    <div @click="minus" class="button operator">-</div>
    <div @click="append('1')" class="button">1</div>
    <div @click="append('2')" class="button">2</div>
    <div @click="append('3')" class="button">3</div>
    <div @click="add" class="button operator">+</div>
    <div @click="append('0')" class="button zero">0</div>
    <div @click="dot" class="button">.</div>
    <div @click="equal" class="button operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '123',
      operator: null,
      operatorClicked: false,
    }
  },

  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      if(this.current.charAt(0) === '-') {
        this.current = this.current.slice(1);
      } 
      
      else {
        this.current = '-' + this.current;
      }
    },
    percentage() {
      this.current = (parseFloat(this.current) / 100).toString();
    },
    append(number) {
      if(this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if(this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },

    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = (this.operator(parseFloat(this.current), parseFloat(this.previous))).toString();
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 500px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color: #4c4c4c;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.button {
  background-color: #d6d6d6;
  border: 1px solid #999;
}

.operator {
  background-color: orange;
  color: white;
}
</style>
