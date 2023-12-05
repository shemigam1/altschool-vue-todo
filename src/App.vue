
<template>
  <div class="max-w-screen flex flex-col items-center justify-center">
    <Header />

    <div class="body border border-slate-900 h-full flex flex-col gap-3 w-2/3 py-4">
      <CreateTodo @createTodo="handleCreateTodo" />
      <TodoList :todos="todos" @deleteTodo="handleDeleteTodo" @editTodo="handleEditTodo" />
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import CreateTodo from './components/CreateTodo.vue'
import TodoList from './components/TodoList.vue'
import Header from './components/Header.vue'
import { onMounted } from 'vue';

const todos = ref([])

const generateUniqueId = () => {
  return Math.floor(Math.random() * 10000000)
}

onMounted(() => {
  const savedTodos = JSON.parse(localStorage.getItem('todos'))

  if (savedTodos) {
    todos.value = savedTodos
  }
})

const saveToLS = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

const handleCreateTodo = (todo) => {
  todos.value.push({
    id: generateUniqueId(),
    todo
  })
  saveToLS()
}

const handleDeleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
  saveToLS()
}

const handleEditTodo = (value) => {
  handleDeleteTodo(value.id)
  handleCreateTodo(value.text)
  saveToLS()
  // console.log(todos.value);
}

</script>
