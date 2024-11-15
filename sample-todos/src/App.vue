<script setup lang="ts">
import { ref } from 'vue'
import type { Todo } from './types'

const todos = ref<Todo[]>([
  { id: 1, text: 'Learn Vue 3 Composition API', completed: false },
  { id: 2, text: 'Build a project', completed: true },
  { id: 3, text: 'Write documentation', completed: false }
])

const newTodo = ref<string>('')

const addTodo = (): void => {
  const text = newTodo.value.trim()
  if (text) {
    const todo: Todo = {
      id: Date.now(),
      text,
      completed: false
    }
    todos.value.push(todo)
    newTodo.value = ''
  }
}

const toggleTodo = (todo: Todo): void => {
  todo.completed = !todo.completed
}
</script>

<template>
  <div class="container mx-auto p-4 max-w-md">
    <h1 class="text-2xl font-bold mb-4">Todo App</h1>
    
    <div class="mb-4">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        type="text"
        placeholder="Add new todo"
        class="border p-2 rounded w-full"
      >
    </div>

    <ul class="space-y-2">
      <li
        v-for="todo in todos"
        :key="todo.id"
        class="flex items-center p-2 border rounded"
      >
        <input
          type="checkbox"
          :checked="todo.completed"
          @change="toggleTodo(todo)"
          class="mr-2"
        >
        <span :class="{ 'line-through': todo.completed }">
          {{ todo.text }}
        </span>
      </li>
    </ul>
  </div>
</template>