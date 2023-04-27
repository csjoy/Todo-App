<script setup lang="ts">
import { defineProps } from 'vue';

interface Obj {
  userId: number;
  id: number;
  title: string;
  completed: boolean;
}

const props = defineProps({
  todos: {
    type: Array<Obj>,
    required: true
  }
})
</script>

<template>
  <ul>
    <li v-for="todo in props.todos" :key="todo.id">
      <slot name="todo" :todo="todo" />
    </li>
  </ul>
</template>