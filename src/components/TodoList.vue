<script setup lang="ts">
import { ref, Ref } from "vue";
import { Todo } from "./TodoItem.model";
import TodoItem from "./TodoItem.vue";

const todos: Ref<Array<Todo>> = ref(
  [
    { id: 1, name: "Buy milk", completed: false },
    { id: 2, name: "Clean house", completed: false },
  ]
);

const onUpdateCompleted = (updatedTodo: Todo) => {
  todos.value = todos.value.map((todo) => {
    if (todo.id === updatedTodo.id) {
      todo = updatedTodo
    }
    return todo
  })
}
</script>

<template>
  <h2>Todo</h2>
  {{ todos }}
  <div
    v-if="todos.length > 0"
    class="todo-list"
  >
    <TodoItem
      v-for="todoItem of todos"
      :key="todoItem.id"
      :todo="todoItem"
      @update-completed="onUpdateCompleted"
    />
  </div>
  <span v-else>Nothing todo</span>
</template>

<style scoped>
.todo-list {
  display: flex;
  flex-direction: column;
}
</style>
