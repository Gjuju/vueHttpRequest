<template>
  <div class="container">
    <div class="left">
      <div>
        <br />
        <h1>Read</h1>
        <br />
        <button @click="reqAll">Request all</button>
        <br />
        <br />
        <input type="number" name="id" id="id" v-model="id" />
        <label for="id">Id</label>
        <button @click="reqId">Request Id</button>
        <br />
        <input type="text" name="name" id="name" v-model="name" />
        <label for="name">Name</label>
        <button @click="reqName">Request Name</button>
        <br />
        <input type="number" name="age" id="age" v-model="age" />
        <label for="age">Age</label>
        <button @click="reqAge">Request Age</button>
        <div v-if="err">{{ err }}</div>
      </div>
      <br />
      <div v-if="list.length > 0">
        <h2>Click one to update/delete</h2>
        <table>
          <thead>
            <tr>
              <th>Id</th>
              <th>Name</th>
              <th>Age</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in list" :key="item.id" @click="showIt(item)">
              <td class="pointer">{{ item.id }}</td>
              <td class="pointer">{{ item.name }}</td>
              <td class="pointer">{{ item.age }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <div class="right">
      <div v-if="selectedItem">
        <UpdateDelete :passedItem="selectedItem" :capitalize="capitalize" />
      </div>
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
  props: {
    capitalize: Function,
  },
  data: function () {
    return {
      id: "",
      name: "",
      age: "",
      selectedItem: undefined,
      ret: "",
      list: [],
      err: "",
    };
  },
  mounted: function () {},
  methods: {
    reqAll: function () {
      this.axios
        .get("https://localhost:7150/api/testitems")
        .then((response) => {
          this.list = response.data.sort((a, b) => {
            return a.id - b.id;
          });
        })
        .catch((err) => {
          console.log("reqAll : ", err);
          this.list = [];
        });
    },
    reqId: function () {
      console.log(this.id);
      let id = this.id;
      this.axios
        .get("https://localhost:7150/api/testitems/" + id)
        .then((response) => {
          if (id == "") {
            this.list = response.data;
          } else {
            this.list = [response.data];
          }
          this.err = "";
        })
        .catch((err) => {
          console.log("reqId : ", err);
          this.err = "Cet Id n'existe pas.";
        });
    },
    reqName: function () {
      console.log(this.name);
      let name = this.capitalize(this.name);
      this.axios
        .get("https://localhost:7150/api/testitems/name/" + name)
        .then((response) => {
          console.log(response)
          if (name != "") {
            this.list = response.data;
          } else {
          this.err = "Veuillez spécifier un nom.";
          }
          this.err = "";
        })
        .catch((err) => {
          console.log("reqName : ", err);
          this.err = "Ce name n'existe pas.";
        });
    },
    reqAge: function () {
      console.log(this.age);
      let age = this.age;
      this.axios
        .get("https://localhost:7150/api/testitems/age/" + age)
        .then((response) => {
          console.log(response)
          if (age != "") {
            this.list = response.data;
          } else {
          this.err = "Veuillez spécifier un nom.";
          }
          this.err = "";
        })
        .catch((err) => {
          console.log("reqName : ", err);
          this.err = "Ce name n'existe pas.";
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
.container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 10px;
  grid-auto-rows: minmax(100px, auto);
}

.left {
  grid-column: 1 / 2;
  grid-row: 1;
}

.right {
  grid-column: 2 / 3;
  grid-row: 1;
}

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
  border: 2px solid #cbcece;
  border-radius: 5px;
  margin: auto;
}

th {
  background-color: #cbcece;
  color: rgba(29, 28, 28, 0.66);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

.pointer {
  cursor: pointer;
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
