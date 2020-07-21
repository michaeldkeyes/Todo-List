<template>
  <div class="container">
    <div class="w-100">
      <h1>Inbox</h1>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <Todo :title="todo.title" :id="todo.id" @deleteTodo="deleteTodo" />
        </li>
        <li>
          <AddView
            v-if="addMode"
            @cancelView="addMode = false"
            @addTodo="addTodo"
          />
          <button type="button" class="m-t-10" v-else @click="addMode = true">
            <i class="fa fa-plus"></i>
            Add Task
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import AddView from "./AddView.vue";
import Todo from "./Todo.vue";

export default {
  name: "TodoList",
  components: {
    AddView,
    Todo,
  },
  data() {
    return {
      addMode: false,
      todos: [],
      id: 0,
    };
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      this.todos = JSON.parse(localStorage.getItem("todos"));

      if (this.todos.length === 0) {
        this.id = 0;
      } else {
        this.id = JSON.parse(localStorage.getItem("id"));
      }
    }
  },
  methods: {
    addTodo(todo) {
      let newTodo = { id: this.id, title: todo, completed: false };
      this.todos.push(newTodo);
      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.id++;
      localStorage.setItem("id", JSON.stringify(this.id));
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
      localStorage.removeItem("todos");
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style lang="scss" scoped>
h1 {
  font-size: 2rem;
  margin-bottom: 8px;
}

ul {
  padding: 0;
  margin: 0;
  width: 100%;
}

button {
  cursor: pointer;
  background-color: transparent;
  border: none;
  color: gray;
  font-size: 1.4rem;
  padding: 4px 0 8px;
  text-align: left;
  width: 100%;
  margin: 0;

  &:hover {
    color: #dd4b39;
  }

  &:hover i {
    color: hsla(0, 0, 100%, 0.87);
    background-color: #dd4b39;
  }
}

i {
  color: #dd4b39;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 17px;
  width: 17px;
  margin-right: 11px;
}

.container {
  display: flex;
  justify-content: center;
  position: relative;
  min-height: 100vh;
  padding: 80px 55px 84px;
  margin: 0 auto;
  width: 100%;
  max-width: 800px;
}

.w-100 {
  width: 100%;
}

.m-t-10 {
  margin-top: 10px;
}
</style>
