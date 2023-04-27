<script setup lang="ts">
const emits = defineEmits(["completeChange"])
const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  completed: {
    type: Boolean,
    required: true,
  },
})
const toggleCompletion = () => {
  const newCompleted = !props.completed
  emits("completeChange", newCompleted)
}
</script>

<template>
  <div class="p-4 shadow-lg my-2 text-lg hover:bg-gray-50 flex justify-between" :class="{ 'line-through': props.completed }">
    <label>{{ props.title }}</label>
    <input type="checkbox" :checked="completed" @change="toggleCompletion">
  </div>
</template>