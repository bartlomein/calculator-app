<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear(), animation('clear')" id = "clear" class="btn">C</div>
    <div @click="sign(), animation('plus-minus')" id = "plus-minus"  class="btn">+/-</div>
    <div @click="percent(),animation('percent')" id = "percent"  class="btn">%</div>
    <div @click="divide(), animation('divide')" id = "divide"  class="btn operator">÷</div>
    <div @click="append('7'),animation('seven')" id = "seven" class="btn">7</div>
    <div @click="append('8'),animation('eight')" id = "eight" class="btn">8</div>
    <div @click="append('9'),animation('nine')" id = "nine" class="btn">9</div>
    <div @click="times(), animation('times')" id = "times" class="btn operator">x</div>
    <div @click="append('4'),animation('four')" id = "four" class="btn">4</div>
    <div @click="append('5'),animation('five')" id = "five" class="btn">5</div>
    <div @click="append('6'),animation('six')" id = "six" class="btn">6</div>
    <div @click="minus(),animation('minus')" id = "minus" class="btn operator">-</div>
    <div @click="append('1'),animation('one')" id = "one" class="btn">1</div>
    <div @click="append('2'),animation('two')" id = "two" class="btn">2</div>
    <div @click="append('3'),animation('three')" id = "three" class="btn">3</div>
    <div @click="add(),animation('add')" id = "add" class="btn operator">+</div>
    <div @click="append('0'),animation('zero')" id = "zero" class="btn zero">0</div>
    <div @click="dot(),animation('dot')" id = "dot" class="btn">.</div>
    <div @click="equal(),animation('equal')" id = "equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.');
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
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
      this.current = `${this.operator(
        parseFloat(this.current), 
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    animation(id){
      let item = document.getElementById(id);
      console.log(item)
      item.classList.add("button-clicked");
      setTimeout(() => {
        this.removeAnimation(id);
      }, 500);
      
      
    },
    removeAnimation(id){
      let itemToRemove = document.getElementById(id);
      itemToRemove.classList.remove("button-clicked");
      console.log(itemToRemove);
    },

  }
}
</script>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}
.button-clicked{

  animation-name: button-grow;
  animation-duration: 0.2s;
}

@keyframes button-grow {
    from {transform: scale(1.0);}
    to {transform: scale(1.1);}
    
}
.btn {
  background-color: #F2F2F2;
  border: 1px solid #999;
}

.operator {
  background-color: orange;
  color: white;
}
</style>