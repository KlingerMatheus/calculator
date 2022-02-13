<template>
  <div id="notification" v-if="!calculatorIsActive">
    <p>Ligue a calculadora! ;)</p>
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
  position: absolute;
  top: 25px;
  right: 25px;
  background-color: rgba(255, 0, 0, 0.3);
  backdrop-filter: blur(2px);
  padding-block: 18px;
  padding-inline: 32px;
  font-weight: bolder;
  text-transform: uppercase;
  border-radius: 4px;
  opacity: 0;
  box-shadow: 0px 3px 3px rgba(0, 0, 0, 0.25);
  animation: floating 2s infinite ease-in-out;
  animation-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
  animation-delay: 2s;
  transition: 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

#notification:hover {
  background-color: rgba(255, 0, 0, 0.8);
}

#notification p {
  color: rgba(255, 255, 255, 0.8);
  text-shadow: 0px 1px 2px rgba(0, 0, 0, 0.5);
}
</style>
