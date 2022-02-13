/* eslint-disable */
<template>
  <div id="led-container">
    <span id="led"></span>
    <span id="led-animation" v-show="calculatorIsActive"></span>
  </div>
</template>

<script>
export default {
  name: "Led",
  props: {
    calculatorIsActive: Boolean,
  },
};
</script>

<style>
/* LED */

#led {
  position: absolute;
  top: 0px;
  left: 0px;
  background-color: rgba(255, 0, 0, 0.2);
  width: 100%;
  height: 0.6%;
  opacity: 1;
}

#led-animation {
  position: absolute;
  top: 0px;
  left: 0px;
  background-color: rgb(255, 0, 0);
  box-shadow: 0px 1px 2px rgb(255, 0, 0);
  width: 100%;
  height: 0.6%;
  opacity: 0;
  animation: fade-in-out 2s infinite ease-in-out;
  animation-delay: 0.6s;
  animation-timing-function: cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
</style>
