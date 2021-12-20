<template>
  <div>
    <button @click="reqAll">request all</button>
    <br />
    <label for="id">Id :</label>
    <input type="number" name="id" id="id" />
    <button @click="reqId">request Id</button>
    <ul>
      <li v-for="item in list" :key="item.id">
        {{ item.id }} - {{ item.name }} - {{ item.age }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RequestReturn",
  props: {},
  data: function () {
    return {
      ret: "",
      list: [],
    };
  },
  methods: {
    reqAll: function () {
      console.log("request All");
      

      this.axios
        .get("https://localhost:7133/api/todoitems")
        .then((response) => {
          console.log(response.data);
        });
    },
    reqId: function () {
      console.log("request Id");
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
