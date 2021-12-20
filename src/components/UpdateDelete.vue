<template>
  <div>
    <br />
    <label for="id">Id :</label>
    <input type="number" name="id" id="id" v-model="item.id"/>
    <br>
    <label for="name">name :</label>
    <input type="text" name="name" id="name" v-model="item.name">
    <br>
    <label for="age">age:</label>
    <input type="text" name="age" id="age" v-model="item.age">
    <br>
    <button @click="deleteItem">delete</button>
    <button @click="updateItem">update item</button>
  </div>
</template>

<script>
export default {
  name: "UpdateDelete",
  props: {
    passedItem: Object
  },
  data: function () {
    return {
      item: this.passedItem,
    };
  },
  methods: {
    deleteItem: function () {
      console.log("delete item : ", this.item);
      this.axios
        .delete("https://localhost:7150/api/todoitems/"+ this.item.id)
        .then((response) => {
           console.log(response.data);
          this.item.id = undefined;
          this.item.name = undefined;
          this.item.age = undefined;
        }).catch( (err) => {console.log(err)});
    },
    updateItem: function () {
      console.log("update item : ", this.item);
      this.axios
        .put("https://localhost:7150/api/todoitems/"+ this.item.id, this.item)
        .then((response) => {
          
           console.log(response.data);
          
        }).catch( (err) => {console.log(err)});
    }
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
