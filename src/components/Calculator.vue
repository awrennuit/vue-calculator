<template>
  <div id="calculator-body">
    <div id="calculator">
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
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      if (this.current === "0" && number === "0") {
        return;
      } else {
        this.current = `${this.current}${number}`;
      }
    },
    clear() {
      this.current = "";
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        if (this.current === "") {
          this.append("0.");
        } else {
          this.append(".");
        }
      }
    },
    equals() {
      this.current = this.operator(+this.previous, +this.current);
      this.previous = null;
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    percent() {
      this.current = `${+this.current / 100}`;
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    sign() {
      // take '' into account
      // take answer into account
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    subtract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#calculator-body {
  background-color: #6d6875;
  border-radius: 4px;
  height: 400px;
  margin: 0 auto;
  padding: 20px 10px 10px 10px;
  width: 400px;
}

#calculator {
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 0 auto;
  width: 400px;
}

#display {
  background-color: #b5838d;
  color: #ffcdb2;
  grid-column: 1 / 5;
  margin: 2px;
  padding-right: 10px;
  text-align: right;
}

#zero {
  grid-column: 1 / 3;
}

.btn {
  background: radial-gradient(#ffcdb2, #ffcdb2, #b5838d);
  border: 1px solid #6d6875;
  border-radius: 6px;
  cursor: pointer;
  margin: 2px;
}

.btn:active {
  background: radial-gradient(#ffcdb2, #b5838d);
}

.operator {
  background: radial-gradient(#e5989b, #e5989b, #b5838d);
}

.operator:active {
  background: radial-gradient(#e5989b, #b5838d);
}
</style>
