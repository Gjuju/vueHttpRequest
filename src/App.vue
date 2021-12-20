<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div class="wrapper">
    <div class="left">
      <Formulaire />
    </div>
    <div class="right">
      <RequestReturn />
    </div>
  </div>
</template>

<script>
import Formulaire from "./components/Formulaire.vue";
import RequestReturn from "./components/RequestReturn.vue";

export default {
  name: "App",
  components: {
    Formulaire,
    RequestReturn,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.wrapper {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 10px;
  grid-auto-rows: minmax(100px, auto);
}
.left {
  grid-column: 1 / 2;
  grid-row: 1;
}
.tight {
  grid-column: 2 / 3;
  grid-row: 1 / 3;
}
</style>
