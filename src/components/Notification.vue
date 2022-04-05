<template>
  <div
    id="notification"
    v-if="!calculatorIsActive"
    title="Ligue a calculadora!"
  >
    <p>Clique na tecla <b class="keywords">ON</b></p>
    <p>
      ou pressione
      <b class="keywords">ESPAÇO</b>
    </p>
  </div>
</template>

<script>
export default {
  name: "Notification",
  props: {
    calculatorIsActive: Boolean,
  },
};
</script>

<style>
/* NOTIFICATION */

#notification {
  position: relative;
  text-align: center;
  margin-bottom: 40px;
  background-color: rgb(200, 0, 0);
  padding: 16px;
  border-radius: 5px;
  opacity: 0;
  box-shadow: 0px 3px 3px rgba(0, 0, 0, 0.25);
  animation: floating 2s infinite ease-in-out;
  animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  animation-delay: 2s;
}

#notification p {
  color: rgb(255, 255, 255);
  font-weight: bolder;
  text-transform: uppercase;
  text-shadow: 0px 1px 2px rgba(0, 0, 0, 0.5);
}

#notification p:first-of-type {
  margin-bottom: 16px;
}

.keywords {
  font-size: 18px;
  background-color: rgb(0, 0, 0);
  border-radius: 100px;
  border: 2px solid rgb(255, 255, 255);
  padding-inline: 8px;
  transition: all 0.5s;
  cursor: grab;
}

.keywords:hover {
  background-color: red;
}
</style>
