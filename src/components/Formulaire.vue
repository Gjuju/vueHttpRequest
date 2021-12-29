<template>
  <div class="hello">
    <div>Create</div>
    <br />
    <label for="name">name : </label>
    <input type="text" name="name" id="name" v-model="name" />
    <p v-if="errName">{{ errName }}</p>
    <br />
    <label for="age">age :</label>
    <input type="number" name="age" id="age" v-model="age" />
    <p v-if="errAge">{{ errAge }}</p>
    <br />
    <button @click="send">submit</button>
  </div>
</template>

<script>
export default {
  name: "Formulaire",
  props: {},
  data: function () {
    return {
      name: "",
      errName: "",
      age: "",
      errAge: "",
    };
  },
  methods: {
    capitalize: function (string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    send: function () {
      let valid = true;
      if (!isNaN(this.name) || this.name == "") {
        this.errName = "Veuillez entrer un nom.";
        valid = false;
      } else {
        this.errName = "";
      }

      if (isNaN(this.age) || this.age == "") {
        this.errAge = "Veuillez entrer un age.";
        valid = false;
      } else {
        this.errAge = "";
      }

      if (valid) {
        console.log(this.name, this.age);
      } else {
        console.log("formulaire invalide !");
        return;
      }

      let content = {
        name: this.capitalize(this.name),
        age: this.age,
      };

      //this.axios.defaults.headers.post['Content-Type'] ='application/json;charset=utf-8';
      //this.axios.defaults.headers.post['Access-Control-Allow-Origin'] = '*';

      this.axios
        .post("https://localhost:7150/api/todoitems", content)
        .then(function (response) {
          console.log("resp : ", response);
        })
        .catch(function (error) {
          console.log("err : ", error);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
