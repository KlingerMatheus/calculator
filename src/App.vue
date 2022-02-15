<template>
  <div id="app">
    <div id="background"></div>
    <div id="page-title">
      <h2>Welcome To The Jungle!</h2>
      <small>Se liga só nessa "simples" calculadora...</small>
    </div>
    <Calculator />
  </div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: { Calculator },
};
</script>

<style scope>
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");

* {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
}

#app {
  font-family: "Roboto", sans-serif;
}

#background {
  position: fixed;
  left: 50%;
  width: 100%;
  height: 100%;
  z-index: -1;
  transform: translateX(-50%);
  background-image: url("./assets/background.jpg");
  background-size: 1920px;
  filter: saturate(0.8);
}

#page-title {
  position: relative;
  background-color: rgba(0, 0, 0, 0);
  padding-block: 15px;
  padding-inline: 30px;
  font-family: "Bebas Neue", cursive;
  color: #fff;
  letter-spacing: 3px;
  font-size: 150%;
  display: flex;
  flex-direction: column;
  align-items: baseline;
  text-shadow: 0px 2px 3px rgba(0, 0, 0, 0.1);
}
</style>
