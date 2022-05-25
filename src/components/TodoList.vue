<template>
  <div>
    <add-todo v-on:add-todo="saveTodo" />
    <div v-bind:key="item.id" v-for="item in todoItems">
      <todo-item
        v-bind:itemInfo="item"
        v-on:del-todo="deleteTodo"
        v-on:change-completion="changeCompletion"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AddTodo from "./AddTodo.vue";
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  components: {
    AddTodo,
    TodoItem,
  },
  data() {
    return {
      todoItems: [
        {
          id: 1,
          title: "Todo 1",
          completed: false,
        },
        {
          id: 2,
          title: "Todo 2",
          completed: true,
        },
        {
          id: 3,
          title: "Todo 3",
          completed: false,
        },
      ],
    };
  },
  methods: {
    saveTodo(newItem) {
      const { title, completed } = newItem;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        .then((res) => (this.todoItems = [...this.todoItems, res.data]))
        .catch((err) => console.log(err));
    },
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          () => (this.todoItems = this.todoItems.filter((todo) => todo.id !== id))
        )
        .catch((err) => console.log(err));
    },
    changeCompletion(id) {
      let todo = this.todoItems.find((item) => item.id === id);
      todo.completed = !todo.completed;
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todoItems = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style scoped>
</style>
