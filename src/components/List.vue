<script>
export default {
  data() {
    return {
      message: "hello",
    };
  },
  props: ["todos"],
};
</script>

<template>
  <ul class="list-group">
    <li
      v-for="(todo, index) in todos"
      class="list-group-item d-flex justify-content-between"
    >
      <div>
        <span v-if="todo.completed === true">
          <del>{{ todo.content }}</del></span
        >
        <span v-else>{{ todo.content }}</span>
      </div>

      <div>
        <button
          v-if="!todo.completed"
          class="btn btn-success"
          @click="$emit('compelteTodo', index)"
        >
          complete
        </button>
        <button
          v-else
          class="btn btn-warning"
          @click="$emit('unCompeleteTodo', index)"
        >
          uncomplete
        </button>
        <button class="btn btn-danger" @click="$emit('deleteTodo', index)">
          X
        </button>
      </div>
    </li>
  </ul>
</template>
