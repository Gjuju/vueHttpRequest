<template>
  <img id="logo" alt="Vue logo" src="./assets/logo.png" />
  <div>
    <Formulaire />
    <br />
    <br />
    <br />
    <RequestReturn />

    <!-- <UpdateDelete /> -->
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
#logo {
  width: 10%;
}
label {
  display: inline-block;
  text-align: center;
  width: 5rem;
}
input {
  margin: 5px 10px 5px 10px;
}
span {
  display: inline-block;
  text-align: center;
  margin-left: 2rem;
}
</style>
