<template>
  <div id="container">
    <span class="meteoro"></span>
    <span class="meteoro-dois"></span>
    <div id="calculator">
      <Led :calculatorIsActive="this.calculatorIsActive" />

      <CalculatorScreen
        :expressionLength="this.expression.length"
        :expression="this.expression"
        :calculatorIsActive="this.calculatorIsActive"
        :dataOnScreen="this.dataOnScreen.toString()"
      />
      <div id="keyboard">
        <table cellspacing="8">
          <tr>
            <td class="key" id="key-on-off" @click="calculatorOnOff()">ON</td>
            <td class="key" @click="clearAll()">C</td>
            <td class="key" @click="backspace()">BS</td>
            <td class="key" @click="addOperators('/')">/</td>
          </tr>
          <tr>
            <td class="key" @click="addNumber('7')">7</td>
            <td class="key" @click="addNumber('8')">8</td>
            <td class="key" @click="addNumber('9')">9</td>
            <td class="key" @click="addOperators('*')">X</td>
          </tr>
          <tr>
            <td class="key" @click="addNumber('4')">4</td>
            <td class="key" @click="addNumber('5')">5</td>
            <td class="key" @click="addNumber('6')">6</td>
            <td class="key" @click="addOperators('+')">+</td>
          </tr>
          <tr>
            <td class="key" @click="addNumber('1')">1</td>
            <td class="key" @click="addNumber('2')">2</td>
            <td class="key" @click="addNumber('3')">3</td>
            <td class="key" @click="addOperators('-')">-</td>
          </tr>
          <tr>
            <td colspan="2" class="key" @click="addNumber('0')">0</td>
            <td class="key" @click="addSeparator()">.</td>
            <td class="key key-equal" @click="equal()">=</td>
          </tr>
        </table>
      </div>
    </div>
    <Notification :calculatorIsActive="this.calculatorIsActive" />
  </div>
</template>

<script>
import Led from "./Led.vue";
import CalculatorScreen from "./Screen.vue";
import Notification from "./Notification.vue";

export default {
  name: "Calculator",
  components: {
    CalculatorScreen,
    Led,
    Notification,
  },
  data: () => {
    return {
      calculatorIsActive: false,
      result: 0,
      dataOnScreen: "",
      expression: [],
    };
  },
  methods: {
    getExpression(value) {
      let string = " ";
      let count = 0;

      for (; count < value.length; count++) {
        string += value[count];
      }

      return string;
    },
    maxLength() {
      if (this.dataOnScreen.length < 12 && this.calculatorIsActive) {
        return true;
      } else {
        return false;
      }
    },
    dataOnScreenIsZero() {
      if (this.dataOnScreen == "") {
        return "0";
      } else {
        return this.dataOnScreen;
      }
    },
    addNumber(value) {
      if (this.maxLength()) {
        console.log(value.length);
        return (this.dataOnScreen += value);
      } else {
        return console.log("Erro.");
      }
    },
    clearAll() {
      return (this.dataOnScreen = ""), (this.expression = []);
    },
    calculatorOnOff() {
      if (this.calculatorIsActive) {
        this.clearCalculator();
        return (this.calculatorIsActive = false);
      } else {
        return (this.calculatorIsActive = true);
      }
    },
    clearCalculator() {
      this.expression = [];
      this.dataOnScreen = "";
      this.result = "";
    },
    backspace() {
      let value = this.dataOnScreen;

      return (this.dataOnScreen = value.substring(0, value.length - 1));
    },
    addOnExpression(number, operator) {
      let expressionLength = this.expression.length;
      let equalValue = Number;
      let asString = String;

      if (expressionLength == 0) {
        this.expression.push(number, operator);
        this.dataOnScreen = "";
      } else if (expressionLength == 3) {
        this.expression = [];
        this.expression.push(number, operator);
        this.dataOnScreen = "";
      } else {
        equalValue = this.calculate();
        asString = equalValue.toString();

        this.expression = [];
        this.expression.push(asString, operator);
        this.dataOnScreen = "";
      }
    },
    addOperators(operator) {
      let number = this.dataOnScreen;

      if (number != "") {
        this.addOnExpression(number, operator);
        return;
      } else {
        this.expression.splice(1, 1);
        this.expression.push(operator);
        return;
      }
    },
    addSeparator() {
      let value = this.dataOnScreen;
      let itHas = value.includes(".");

      if (!itHas) {
        if (this.dataOnScreen == "") {
          return (this.dataOnScreen += "0.");
        } else {
          return (this.dataOnScreen += ".");
        }
      }
    },
    numberParse(string) {
      return parseFloat(string);
    },
    equal() {
      let number = this.dataOnScreen;

      this.expression.push(number);
      this.dataOnScreen = this.calculate();
    },
    calculate() {
      let n1 = this.numberParse(this.expression[0]);
      let n2 = this.numberParse(this.dataOnScreen);
      let operator = this.expression[1];
      let equal = Number;

      switch (operator) {
        case "+": {
          equal = n1 + n2;
          break;
        }
        case "-": {
          equal = n1 - n2;
          break;
        }
        case "*": {
          equal = n1 * n2;
          break;
        }
        case "/": {
          if (n2 != 0) {
            equal = n1 / n2;
          } else {
            alert("Impossível dividir por 0(Zero).");
            return;
          }
          break;
        }
      }

      return equal;
    },
  },
};
</script>

<style>
body {
  overflow: hidden;
}

/* CONTAINER */

#container {
  display: flex;
  align-items: center;
  flex-direction: column;
  user-select: none;
  overflow: hidden;
}

/* CALCULATOR */

#calculator {
  position: relative;
  backdrop-filter: blur(3px);
  padding: 16px;
  box-shadow: 0px 8px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  transition: 1s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  margin-top: 15px;
  margin-bottom: 25px;
  overflow: hidden;
}

#calculator:hover {
  transform: translateY(-15px);
  background-color: rgba(255, 255, 255, 0.1);
}

#expression {
  position: absolute;
  font-size: 22px;
  top: 0px;
  right: 8px;
  font-weight: 600;
}

/* KEYBOARD */

#keyboard tr td {
  padding: 12px;
  font-size: 22px;
  font-weight: bold;
  text-align: center;
  width: 50px;
  height: 50px;
  transition: 0.1s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  border-radius: 3px;
  color: #fff;
  text-shadow: 0px 2px 2px rgba(0, 0, 0, 0.5);
  margin-inline: -10px;
}

#keyboard tr td:hover {
  background-color: rgba(255, 255, 255, 0.2);
  box-shadow: 0px 0px 3px rgba(0, 0, 0, 0.25);
  cursor: pointer;
}

#keyboard tr td:active {
  box-shadow: inset 0px 0px 60px rgba(0, 0, 0, 0.3);
}

.key-equal {
  background-color: rgba(30, 120, 255, 0.75);
}

/* METEORO */

.meteoro,
.meteoro-dois {
  position: absolute;
  opacity: 0;
  background-image: url("../assets/meteoro.png");
  background-repeat: no-repeat;
  width: 500px;
  height: 500px;
  filter: brightness(1.6);
  z-index: 0;
}

.meteoro {
  animation: 16s meteoro infinite;
  top: -200px;
  right: -300px;
  animation-delay: 3s;
  transform: rotate(140deg) scale(0.4);
}

.meteoro-dois {
  top: -300px;
  right: -200px;
  animation: 16s meteoro-dois infinite;
  animation-delay: 3.6s;
  transform: rotate(140deg) scale(0.2);
}

/* ANIMATIONS */

@keyframes meteoro {
  0% {
    opacity: 0;
  }
  1% {
    opacity: 0.6;
  }
  6% {
    top: -100px;
    right: 100%;
    opacity: 0.6;
  }
  7% {
    opacity: 0;
  }
}

@keyframes meteoro-dois {
  0% {
    opacity: 0;
  }
  1% {
    opacity: 0.6;
  }
  6% {
    top: -100px;
    right: 100%;
    opacity: 0.6;
  }
  7% {
    opacity: 0;
  }
}

@keyframes floating {
  0% {
    transform: rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  20% {
    transform: rotate(2deg);
  }
  30% {
    transform: rotate(-2deg);
  }
  50% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(0deg);
    opacity: 1;
  }
}

@keyframes fade-in-out {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }

  100% {
    opacity: 0;
  }
}

/* RESPONSIVE */

@media screen and (max-width: 600px) {
  #calculator {
    margin-top: -50px;
    transform: scale(0.7);
  }

  #calculator:hover {
    transform: translateY(-10px) scale(0.7);
  }

  #notification {
    font-size: 11px;
  }
}

@media screen and (max-width: 768px) {
  #notification {
    position: static;
    margin-top: -15px;
    margin-bottom: 10px;
  }
}
</style>
