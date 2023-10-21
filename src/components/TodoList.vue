<template>
  <div class="todo-list-wrapper">
    <div class="todo-list">
      <h1>Lista de Tarefas</h1>
      <div class="input-wrapper">
        <div className="image">➕</div>
        <input type="text" @change="addToList" v-model="text" />
      </div>
      <ul>
        <ListItem
          v-for="(item, index) in list"
          :key="index"
          :item="item"
          :index="index"
          @delete-item="deleteFromList"
          v-model="item.checked"
          @updateStore="updateLocalStrorage"
        />
      </ul>
    </div>
  </div>
</template>

<script>
import ListItem from "./ListItem.vue";

export default {
  name: "TodoList",
  components: {
    ListItem,
  },
  data() {
    return {
      list: [],
      text: "",
    };
  },
  created() {
    this.list = JSON.parse(localStorage.getItem("list")) || [];
  },
  methods: {
    addToList() {
      this.list.unshift({ label: this.text, checked: false });
      this.updateLocalStrorage();
      this.text = "";
    },
    deleteFromList(index) {
      this.list.splice(index, 1);
      this.updateLocalStrorage();
    },
    updateLocalStrorage() {
      localStorage.setItem("list", JSON.stringify(this.list));
    },
  },
};
</script>

<style scoped>
.todo-list-wrapper {
  background-color: #17181f;
  color: #797a81;
  min-height: 100vh;
}

.todo-list {
  max-width: 980px;
  padding: 10px;
  margin: auto;
}

h1 {
  text-align: center;
  color: white;
  padding: 40px 0 10px;
  margin: 0;
}

.input-wrapper {
  display: flex;
  align-items: center;
  border: 1px solid #555;
  border-radius: 15px;
  padding: 12px 15px;
  margin: 20px 0;
}

input {
  border: 0px;
  background: transparent;
  outline: 0;
  color: #fff;
  font-size: 16px;
  flex: 1;
  margin-left: 5px;
}

ul {
  list-style: none;
  padding: 0;
}
</style>
