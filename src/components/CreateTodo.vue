<template>
    <div class="flex gap-7 w-full justify-center self-start">
        <input v-model="todo" class="h-11 border-slate-300 focus:border-slate-600 border rounded w-3/5" type="text"
            name="new-todo" id="">
        <button @click="createTodo"
            class="border rounded bg-slate-800 hover:bg-red-600 text-white text-center h-11 px-6 w-1/5">New</button>

    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['createTodo'])

const todo = ref("")

const createTodo = () => {
    if (!todo.value) {
        return
    }

    emit('createTodo', todo.value)
    todo.value = ""
}
</script>