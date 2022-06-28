<script>
import List from "./components/List.vue";
export default {
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  methods: {
    // add new todo
    add() {
      this.todos.unshift({
        content: this.todo,
        completed: false,
      });
      this.todo = "";
      this.saveToLocal();
    },
    // complete todo
    compelteTodo(indexOfTodo) {
      this.todos = this.todos.map((todo, index) => {
        if (index === indexOfTodo) {
          todo.completed = true;
        }
        return todo;
      });
      this.saveToLocal();
    },
    // delete todo
    deleteTodo(indexOfTodo) {
      this.todos = this.todos.filter((todo, index) => {
        if (indexOfTodo !== index) {
          return todo;
        }
      });
      this.saveToLocal();
    },
    // un complete todo
    unCompeleteTodo(indexOfTodo) {
      this.todos = this.todos.map((todo, index) => {
        if (index === indexOfTodo) {
          todo.completed = false;
        }
        return todo;
      });
      this.saveToLocal();
    },
    // save todo to local storage
    saveToLocal() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
  // components
  components: {
    List,
  },
  // get todo from local storage
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"));
  },
  // get todos length
  computed: {
    getTodoNum() {
      return this.todos.length;
    },
  },
};
</script>

<template>
  <div class="container bg-success mt-5">
    <div class="card">
      <div class="card-body">
        <h4 class="card-title text-center text-capitalize">to do app</h4>
        <!-- input todo -->
        <div class="row mt-3">
          <!--  input  -->
          <div class="col-10">
            <input
              type="text"
              v-model="todo"
              class="form-control"
              placeholder="add new todo"
              @keyup.enter="add"
            />
          </div>
          <!--  btn -->
          <div class="col-2">
            <button class="btn btn-primary" @click="add">add</button>
          </div>
        </div>
        <!-- todo list -->
        <div class="row mt-3">
          <div class="col">
            <List
              :todos="todos"
              @compelteTodo="compelteTodo"
              @deleteTodo="deleteTodo"
              @unCompeleteTodo="unCompeleteTodo"
            />
          </div>
        </div>
        <p class="text-center mt-3">
          total todos number: <span class="text-primary">{{ getTodoNum }}</span>
        </p>
      </div>
    </div>
  </div>
</template>
