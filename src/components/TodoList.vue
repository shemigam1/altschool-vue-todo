<template>
    <ul>
        <li v-for="todo in todos" class="flex justify-center font-semibold " :key="todo.id">
            <div class="rounded flex flex-col items-center border border-red-500 w-4/5 bg-slate-300">
                <div class="flex gap-3">
                    <input class="" @click="lineThrough(todo.id)" type="checkbox" name="">
                    <p v-if="toBeEdited === false" :id="todo.id" class="h-8 text-xl">{{ todo.todo }}</p>
                    <p v-else="" :id="todo.id" class="h-8 text-xl">{{ editedTodo }}</p>


                </div>
                <div class="flex gap-3" v-show="toBeEdited">
                    <input class="border-red-500 border rounded" v-model="editedTodo" id="newtodo" type="text">
                    <button @click="saveEdit(editedTodo, todo.id)"
                        class="w-1/2 border px-4 rounded hover:bg-green-400 border-slate-950 text-2xl text-center">Done</button>
                </div>
                <div class="w-full h-8 flex">
                    <button @click="onEditTodo(todo.todo, todo.id)"
                        class="w-1/2 hover:bg-red-700 text-2xl text-center">Edit</button>
                    <button @click="onDeleteTodo(todo.id)"
                        class="w-1/2 hover:bg-red-700 text-2xl text-center">Delete</button>
                </div>
            </div>
        </li>
    </ul>
</template>

<script setup>
import { ref } from 'vue'

const editedTodo = ref("")
// const toBeEdited = ref({})
// const editedTodo = ref({})
const toBeEdited = ref(false)

const props = defineProps({
    todos: {
        type: Array,
        required: true
    }
})

const emit = defineEmits(['deleteTodo', 'editTodo'])

const onDeleteTodo = (id) => {
    emit('deleteTodo', id)
}
const onEditTodo = (value, id) => {
    // console.log('Editing todo with ID:', id, 'and new value:', value);
    if (toBeEdited.value === false) {
        toBeEdited.value = true
    }
    else {
        toBeEdited.value = false
    }
    // const newTodoData = ref({ id, value })
    const newTodo = document.getElementById('newtodo')
    newTodo.value = value
    editedTodo.value = value

    // toBeEdited = false
}

const saveEdit = (text, id) => {
    toBeEdited.value = !(toBeEdited.value)
    // todo.todo = text
    emit('editTodo', { text, id })
}


const lineThrough = (id) => {
    const line = document.getElementById(id)
    line.classList.toggle('line-through')
}
</script>

