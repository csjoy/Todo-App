<script setup lang="ts">
interface Obj {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}

import { ref, onMounted } from 'vue';
import TodoList from './components/TodoList.vue';
import TodoEntry from './components/TodoEntry.vue';

let todos = ref<Obj[]>([])

onMounted(async () => {
  const response = await fetch("https://jsonplaceholder.typicode.com/todos")
  todos.value = await response.json()
})

const handleCompleteChange = (id: number, newCompleted: any) => {
  todos.value = todos.value.map((todo: Obj) => todo.id === id ? { ...todo, completed: newCompleted } : todo)
}
</script>

<template>
  <div class="container mx-auto">
    <h1 class="text-4xl font-bold text-center my-4">Todo App</h1>
    <TodoList :todos="todos">
      <template #todo="{ todo }">
        <TodoEntry :id="todo.id" :title="todo.title" :completed="todo.completed" @completeChange="handleCompleteChange(todo.id, $event)" />
      </template>
    </TodoList>
  </div>
</template>
