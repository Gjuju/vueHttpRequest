<template>
  <div>
    <div>
      <div>Read</div>
      <br />
      <button @click="reqAll">request all</button>
      <br />
      <label for="id">Id :</label>
      <input type="number" name="id" id="id" v-model="id" />
      <button @click="reqId">request Id</button>
    </div>

    <div>
      <table>
        <thead>
          <tr>
            <th>id</th>
            <th>name</th>
            <th>age</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in list" :key="item.id" @click="showIt(item)">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.age }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div v-if="selectedItem">
      <UpdateDelete :passedItem="selectedItem" />
    </div>
  </div>
</template>

<script>
import UpdateDelete from "./UpdateDelete.vue";

export default {
  name: "RequestReturn",
  components: {
    UpdateDelete,
  },
  props: {},
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
          this.list = response.data;
        });
    },
    reqId: function () {
      console.log("request Id: ", this.id);
      let id = this.id;
      this.axios
        .get("https://localhost:7150/api/todoitems/" + id)
        .then((response) => {
          if (id == "") {
            this.list = response.data;
          } else {
            this.list = [response.data];
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
    showIt: function (item) {
      this.clearState().then(() => {
        this.selectedItem = item;
      });
    },
    clearState: async function () {
      this.selectedItem = undefined;
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

table {
  border: 2px solid #8d9290;
  border-radius: 5px;
  margin: auto;
}

th {
  background-color: #8d9290;
  color: rgba(255, 255, 255, 0.66);
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}

th.active {
  color: #fff;
}

th.active .arrow {
  opacity: 1;
}
</style>
