<template>
  <div class="calculadora">
    <div class="display">{{current || 0}}</div>
    <div @click="clear" class="btn funcoes">AC</div>
    <div @click="change" class="btn funcoes">+/-</div>
    <div @click="percent" class="btn funcoes">%</div>
    <div @click="divide" class="btn operadores">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="mult" class="btn operadores">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operadores">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn operadores">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operadores">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClick: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    change() {
      this.current = this.current.charAt(0) === '-' ?
         this.current.slice(1) : `-${this.current}`
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append(number) {
      if(this.operatorClick) {
        this.current = ''
        this.operatorClick = false
      }
      this.current = `${this.current}${number}`
    },
    dot() {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious() {
    this.previous = this.current
    this.operatorClick = true
    },
    divide() {
    this.operator = (a, b) => a / b
    this.setPrevious()
    },
    mult() {
    this.operator = (a, b) => a * b
    this.setPrevious()
    },
    minus() {
    this.operator = (a, b) => a - b
    this.setPrevious()
    },
    plus() {
    this.operator = (a, b) => a + b
    this.setPrevious()
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
    )}`
    this.previous = null
    }
  }

}
</script>


<style scoped>
.calculadora {
  border: 1px solid black;
  border-radius: 10px;
  margin: 0 auto;
  width: 500px;
  height: 650px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color:white;
  border-radius: 10px;
}
.zero{
  grid-column: 1 / 3;
  border-radius: 0 0 0 10px;

}
.btn {
  background-color: aqua;
  cursor: pointer;
}
.operadores {
  background-color: #349392;
}
.funcoes {
  background-color: #76b7be;
}

</style>
