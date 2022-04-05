<template>
  <div id="screen">
    <div v-if="expressionLength > 0" id="expression">
      <small>{{ this.getExpression(expression) }}</small>
    </div>
    <div id="user-entry">
      <p v-if="calculatorIsActive">{{ dataOnScreenIsEmpty() }}</p>
      <p v-else-if="!calculatorIsActive">OFF</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "CalculatorScreen",
  props: {
    expressionLength: Number,
    expression: Array,
    calculatorIsActive: Boolean,
    dataOnScreen: String,
  },
  methods: {
    dataOnScreenIsEmpty() {
      if (this.dataOnScreen == "") {
        return "0";
      } else {
        return this.dataOnScreen;
      }
    },
    getExpression(value) {
      let string = " ";
      let count = 0;

      for (; count < value.length; count++) {
        string += value[count];
      }

      return string;
    },
  },
};
</script>

<style scope>
/* SCREEN */

#screen {
  background-color: #fff;
  padding: 6px;
  padding-top: 18px;
  font-size: 47px;
  text-align: right;
  font-weight: thin;
  border-radius: 4px;
  margin-bottom: 20px;
  position: relative;
}
</style>
