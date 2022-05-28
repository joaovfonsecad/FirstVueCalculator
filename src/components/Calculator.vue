<template>
  <div class="calculator">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equals" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: "IDontUnderstand",
  data() {
    return {
      current: "",
      previous: "",
      operation: null,
      clicked: false,
      buttonClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      if (this.current !== "") {
        this.current =
          this.current.charAt(0) === "-"
            ? this.current.slice(1)
            : `-${this.current}`;
      }
    },
    percent() {
      this.current = this.current * 0.01;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.current = `${this.current}.`;
      }
    },
    append(number) {
      if (this.clicked) {
        this.current = "";
        this.clicked = false;
      }
      if (this.current === "" && number !== "0") {
        this.current = `${this.current}${number}`;
      } else if (this.current !== "") {
        this.current = `${this.current}${number}`;
      }
    },
    setOperation() {
      if (!this.clicked) {
        this.previous = this.current;
        this.clicked = true;
      } else {
        this.equals();
      }
    },
    divide() {
      this.setOperation();
      this.operation = (a, b) => a / b;
    },
    multiply() {
      this.setOperation();
      this.operation = (a, b) => a * b;
    },
    subtract() {
      this.setOperation();
      this.operation = (a, b) => a - b;
    },
    add() {
      this.setOperation();
      this.operation = (a, b) => a + b;
    },
    equals() {
      this.current = `${this.operation(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  margin: 0 auto;
  width: 250px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 1.7em;
  caret-color: transparent;
  box-shadow: 0 0 2em #333;
}

.display {
  grid-column: 1 / 5;
  background: #666;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 1em;
  height: 2.5em;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  border: 1px solid #999;
  background: #ddd;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.operator {
  background: orange;
  color: white;
}
</style>
