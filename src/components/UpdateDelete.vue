<template>
  <div>
    <br />
    <br />
    <br />
    <div>Update / Delete</div>
    <br />
    <label for="id">Id :</label>
    <input type="number" name="id" id="id" v-model="tempItem.id" />
    <br />
    <label for="name">name :</label>
    <input type="text" name="name" id="name" v-model="tempItem.name" />
    <br />
    <label for="age">age:</label>
    <input type="text" name="age" id="age" v-model="tempItem.age" />
    <br />
    <button @click="deleteItem">delete</button>
    <button @click="updateItem">update item</button>
  </div>
</template>

<script>
export default {
  name: "UpdateDelete",
  props: {
    passedItem: Object,
  },
  data: function () {
    return {
      item: this.passedItem,
      tempItem: { ...this.passedItem },
    };
  },
  methods: {
    capitalize: function (string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
    deleteItem: function () {
      this.axios
        .delete("https://localhost:7150/api/todoitems/" + this.item.id)
        .then((response) => {
          console.log(response.data);
          this.item.id = undefined;
          this.item.name = undefined;
          this.item.age = undefined;
        })
        .catch((err) => {
          console.log("deleteItem : ", err);
        });
    },
    updateItem: function () {
      this.tempItem.name = this.capitalize(this.tempItem.name);
      console.log("update item : ", this.item, " to : ", this.tempItem);
      this.axios
        .put(
          "https://localhost:7150/api/todoitems/" + this.tempItem.id,
          this.tempItem
        )
        .then((response) => {
          console.log(response.data);
        })
        .catch((err) => {
          console.log("updateItem : ", err);
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
