<template>
  <div>
    <br />
    <br />
    <br />
    <br />
    <br />
    <h1>Update / Delete</h1>
    <br />
    <input type="number" readonly name="id" id="id" v-model="tempItem.id" />
    <label for="id">Id</label>
    <br />
    <input type="text" name="name" id="name" v-model="tempItem.name" />
    <label for="name">Name</label>
    <br />
    <input type="text" name="age" id="age" v-model="tempItem.age" />
    <label for="age">Age</label>
    <br />
    <button @click="updateItem">Update item</button>
    <button @click="deleteItem">Delete item</button>
    <div v-if="returnMsg != ''">{{ returnMsg }}</div>
  </div>
</template>

<script>
export default {
  name: "UpdateDelete",
  props: {
    passedItem: Object,
    capitalize: Function

  },
  data: function () {
    return {
      item: this.passedItem,
      tempItem: { ...this.passedItem },
      returnMsg: "",
    };
  },
  methods: {
    
    deleteItem: function () {
      this.axios
        .delete("https://localhost:7150/api/testitems/" + this.tempItem.id)
        .then((response) => {
          console.log(response.data);
          this.tempItem.id = undefined;
          this.tempItem.name = undefined;
          this.tempItem.age = undefined;
          this.returnMsg = "L'entrée a bien été supprimée.";
        })
        .catch((err) => {
          console.log("deleteItem : ", err);
          this.returnMsg = "Une erreur s'est produite !";
        });
    },
    updateItem: function () {
      this.tempItem.name = this.capitalize(this.tempItem.name);
      this.axios
        .put(
          "https://localhost:7150/api/testitems/" + this.tempItem.id,
          this.tempItem
        )
        .then((response) => {
          console.log(response.data);
          this.tempItem.id = undefined;
          this.tempItem.name = undefined;
          this.tempItem.age = undefined;
          this.returnMsg = "L'entrée a bien été  mise à jour.";
        })
        .catch((err) => {
          console.log("updateItem : ", err);
          this.returnMsg = "Une erreur s'est produite !";
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
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
