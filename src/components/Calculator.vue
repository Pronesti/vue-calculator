<template>
  <div class="calculator">
    <input class="visor" disabled v-model="visorView" />
    <div class="wrapper">
      <button class="ac light" @click="clearVisor">AC</button>
      <button class="posneg light" @click="changeToPosNeg">+/-</button>
      <button class="percent light" @click="doOperation('percent')">%</button>
      <button class="divide orange" @click="doOperation('divide')">/</button>
      <button class="seven" @click="clickNumber(7)">7</button>
      <button class="eight" @click="clickNumber(8)">8</button>
      <button class="nine" @click="clickNumber(9)">9</button>
      <button class="multiply orange" @click="doOperation('multiply')">
        x
      </button>
      <button class="four" @click="clickNumber(4)">4</button>
      <button class="five" @click="clickNumber(5)">5</button>
      <button class="six" @click="clickNumber(6)">6</button>
      <button class="substract orange" @click="doOperation('substract')">
        -
      </button>
      <button class="one" @click="clickNumber(1)">1</button>
      <button class="two" @click="clickNumber(2)">2</button>
      <button class="three" @click="clickNumber(3)">3</button>
      <button class="plus orange" @click="doOperation('plus')">+</button>
      <button class="zero" @click="clickNumber(0)">0</button>
      <button class="point" @click="clickNumber('.')">.</button>
      <button class="equals orange" @click="equals">=</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data: function () {
    return {
      currentNumber: [],
      currentSign: "+",
      numberOne: 0,
      numberTwo: 0,
      operation: "",
      result: null,
    };
  },
  computed: {
    visorView: function () {
      if (this.result !== null) return this.result;
      if (this.currentNumber.length < 1) return 0;
      if (this.currentSign == "-")
        return this.currentSign + this.currentNumber.join("");
      return this.currentNumber.join("");
    },
  },
  methods: {
    clickNumber: function (number) {
      this.currentNumber.push(number);
      this.result = null;
    },
    clearVisor: function () {
      this.operation = "";
      this.currentSign = "+";
      this.currentNumber = [];
      this.result = null;
    },
    doOperation: function (operation) {
      if (this.result == "ERROR") this.cleanVariables();
      if (this.currentNumber.length < 1) this.currentNumber = ["0"];
      if (this.currentSign == "+") {
        this.numberOne = parseFloat(this.currentNumber.join(""));
      } else {
        this.numberOne = parseFloat("-" + this.currentNumber.join(""));
      }
      this.clearVisor();
      this.operation = operation;
    },
    changeToPosNeg: function () {
      if (this.currentSign == "+") {
        this.currentSign = "-";
      } else {
        this.currentSign = "+";
      }
    },
    equals: function () {
      if (this.currentNumber.length < 1) this.currentNumber = ["0"];
      if (this.currentSign == "+") {
        this.numberTwo = parseFloat(this.currentNumber.join(""));
      } else {
        this.numberTwo = parseFloat("-" + this.currentNumber.join(""));
      }
      if (this.operation == "plus") {
        this.result = this.numberOne + this.numberTwo;
      } else if (this.operation == "substract") {
        this.result = this.numberOne - this.numberTwo;
      } else if (this.operation == "multiply") {
        this.result = this.numberOne * this.numberTwo;
      } else if (this.operation == "divide") {
        this.result = this.numberOne / this.numberTwo;
        if (this.numberTwo == 0) this.result = "ERROR";
      } else if (this.operation == "percent") {
        this.result = (this.numberOne * this.numberTwo) / 100;
      }
      this.cleanVariables();
      this.currentNumber = ("" + this.result).split("");
    },
    cleanVariables: function () {
      this.currentNumber = [];
      this.currentSign = "+";
      this.numberOne = 0;
      this.numberTwo = 0;
      this.operation = "";
    },
  },
  props: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 15rem;
  padding: 1rem;
  background-color: black;
  border-radius: 5%;
}

.wrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 0.1rem;
  grid-auto-rows: minmax(2rem, auto);
  grid-auto-columns: minmax(2rem, auto);
  width: 10rem;
  margin: 0.1rem;
}

.wrapper button {
  color: white;
  border-radius: 50%;
  background-color: rgb(66, 63, 63);
  height: 3rem;
  width: 3rem;
  border: none;
  margin: 0.2rem;
  font-size: 1.3rem;
}

.sign {
  color: white;
  display: inline;
  float: left;
  font-size: 1.3rem;
}

.visor {
  display: inline;
  width: 10rem;
  height: 1.5rem;
  display: block;
  margin-bottom: 1rem;
  background-color: black;
  border: none;
  color: white;
  font-size: 2rem;
  text-align: right;
}

.equals {
  grid-row: 2/5;
}

.zero {
  grid-column: 2/4;
  width: 6rem;
}

.ac {
  grid-column: 1;
  grid-row: 1;
}

.posneg {
  grid-column: 2;
  grid-row: 1;
}

.percent {
  grid-column: 3;
  grid-row: 1;
}

.divide {
  grid-column: 4;
  grid-row: 1;
}

.multiply {
  grid-column: 4;
  grid-row: 2;
}

.seven {
  grid-column: 1;
  grid-row: 2;
}

.substract {
  grid-column: 4;
  grid-row: 3;
}

.plus {
  grid-column: 4;
  grid-row: 4;
}
.equals {
  grid-column: 4;
  grid-row: 5;
}

.zero {
  grid-column: 1/3;
  grid-row: 5;
  width: 6rem !important;
  border-radius: 45% !important;
}

.point {
  grid-column: 3;
  grid-row: 5;
}

.orange {
  background-color: orange !important;
}

.light {
  background-color: rgb(131, 130, 130) !important;
  color: rgb(48, 47, 47) !important;
}
</style>
