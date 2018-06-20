<template>
  <div class="calculator">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class = "button">C</div>
    <div @click="sign" class = "button">+/-</div>

    <div @click="percent" class = "button">%</div>
    <div class = "button operator">÷</div>
    <div class = "button">7</div>
    <div class = "button">8</div>
    <div class = "button">9</div>
    <div class = "button operator">*</div>
    <div class = "button">4</div>
    <div class = "button">5</div>
    <div class = "button">6</div>
    <div class = "button operator">-</div>
    <div class = "button">1</div>
    <div class = "button">2</div>
    <div class = "button">3</div>
    <div class = "button operator">+</div>
    <div class = "zero button">0</div>
    <div class = "button">.</div>
    <div class = "button operator">=</div>
   </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
    };
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `- ${this.current}`;
    },
    percent(){
      this.current = `${parseFloat(this.current)/100}`;
    },
    append(number){
       this.current = `${this.current}${number}`
    }
  }
};
</script>


<style scoped>
.calculator {
  max-width: 30%;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, atuo);
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}

.zero {
  grid-column: 1/3;
}
.button {
  background-color: #eee;
  border: 0.5px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
