<template>
  <div>
    <div>


    <button @click="reqAll">request all</button>
    <br />
    <label for="id">Id :</label>
    <input type="number" name="id" id="id" v-model="id"/>
    <button @click="reqId">request Id</button>
    <ul>
      <li v-for="item in list" :key="item.id" @click="showIt(item)">
        {{ item.id }} - {{ item.name }} - {{ item.age }}
      </li>
    </ul>
    </div>
    <div v-if="selectedItem">
      <UpdateDelete :passedItem="selectedItem"/>
    </div>
  </div>
</template>

<script>
import UpdateDelete from "./UpdateDelete.vue";

export default {
  name: "RequestReturn",
  components:{
    UpdateDelete
  },
  props: {
    },
  data: function () {
    return {
      id: "",
      selectedItem: undefined,
      ret: "",
      list: [],
    };
  },
  methods: {
    reqAll: function () {
      console.log("request All");
      this.axios
        .get("https://localhost:7150/api/todoitems")
        .then((response) => {
          this.list = response.data
        });
    },
    reqId: function () {
      console.log("request Id: ", this.id);
      let id = this.id
      this.axios
        .get("https://localhost:7150/api/todoitems/"+ id)
        .then((response) => {
          if (id == "") {
            this.list = response.data
          } else {
            this.list = [response.data]
          }
        }).catch( (err) => {console.log(err)});
    },
    showIt: function (item) {
      this.clearState().then(() => {
        this.selectedItem = item
      })
    },
    clearState: async function () {
      this.selectedItem = undefined;
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
