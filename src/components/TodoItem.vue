<script setup lang="ts">
import {computed} from 'vue'
import { Todo } from './TodoItem.model';

const props = defineProps<{
  todo: Todo;
}>();

const emit = defineEmits<{
  (e: 'update-completed', value: Todo): void
}>()

const completedInputModel = computed({
  // getter
  get() {
    return props.todo.completed
  },
  // setter
  set(newValue: boolean) {
    emit('update-completed', {...props.todo, completed: newValue})
  }
})
</script>

<template>
  <div class="container">
    <p>{{ todo.name }}</p>
    Completed?
    <!-- ⚠️ Enable this line to see the ESLint error
      <input
      v-model="todo.completed"
      type="checkbox"
    /> -->
    <input
      v-model="completedInputModel"
      type="checkbox"
    />
  </div>
</template>

<style scoped>
.container {
  border: 1px solid white;
  border-radius: 10px;
  padding: 10px;
}
</style>
