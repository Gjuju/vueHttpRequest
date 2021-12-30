<template>
  <h2 id="title">
    <img id="logo" alt="Vue logo" src="./assets/logo.png" /> DotNet Rest Api
    test client
  </h2>
  <br />
  <div>
    <Formulaire :capitalize="capitalize" />
    <RequestReturn :capitalize="capitalize" />
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
  methods: {
    capitalize: function (string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
  }
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
  width: 40px;
  vertical-align: middle;
}
label {
  display: inline-block;
  text-align: start;
  width: 4rem;
  font-weight: bold;
}
input {
  margin: 5px 10px 5px 10px;
}
span {
  display: inline-block;
  text-align: center;
  margin-left: 2rem;
}

button {
  background-color: #41b883;
  border-radius: 8px;
  border: 1px solid #18ab29;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 17px;
  padding: 6px 12px;
  text-decoration: none;
  text-shadow: 0px 1px 0px #2f6627;
  margin: 0px 1rem 0px 1rem;
}
button:hover {
  background-color: #5cbf2a;
}
button:active {
  position: relative;
  top: 1px;
}

input {
  padding: 6px 12px;
}
</style>
