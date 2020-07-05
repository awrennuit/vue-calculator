<template>
  <div class="calculator">
    <div id="display">{{ current || "0" }}</div>

    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">÷</div>

    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="multiply">x</div>

    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="subtract">-</div>

    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>

    <div class="btn" id="zero" @click="append('0')">0</div>
    <div class="btn" @click="dot">.</div>
    <div class="btn operator" @click="equals">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      operator: null,
      operatorClicked: false,
      previous: null,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      // take '' into account
      // take answer into account
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${+this.current / 100}`;
    },
    append(number) {
      // take '' and 0 into account
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      this.current.indexOf(".") === -1 ? this.append(".") : null;
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    equals() {
      this.current = this.operator(+this.previous, +this.current);
      this.previous = null;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#display {
  background-color: pink;
  grid-column: 1 / 5;
}

#zero {
  grid-column: 1 / 3;
}

.calculator {
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  width: 400px;
}

.btn {
  background-color: #f2f2f2;
  border: 1px solid #999;
}

.operator {
  background: orange;
  color: white;
}
</style>
