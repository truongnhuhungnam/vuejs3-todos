<template>
    <ul>
        <BaseTodosFormAdd @todo-add="addTodo" />
        <BaseTodosItem
            v-for="todo in todos"
            :key="todo.id"
            :todoProps="todo"
            @todo-completed="markCompleted"
            @todo-delete="deleteTodo"
        />
    </ul>
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'
import BaseTodosItem from '../Todos/BaseTodosItem'
import BaseTodosFormAdd from './BaseTodosFormAdd'
export default {
    components: { BaseTodosItem, BaseTodosFormAdd },
    setup() {
        const todos = ref([])

        const getAllTodos = async () => {
            try {
                const res = await axios.get(
                    'https://60a8d18120a6410017306479.mockapi.io/vue3todos'
                )
                todos.value = res.data
            } catch (error) {
                console.log(error)
            }
        }

        getAllTodos()

        const markCompleted = (id) => {
            todos.value = todos.value.map((todo) => {
                if (todo.id === id) todo.completed = !todo.completed
                return todo
            })
        }

        const deleteTodo = async (id) => {
            try {
                await axios.delete(
                    `https://60a8d18120a6410017306479.mockapi.io/vue3todos/${id}`
                )
                todos.value = todos.value.filter((todo) => todo.id !== id)
            } catch (error) {
                console.log(error)
            }
        }

        const addTodo = async (newTodo) => {
            try {
                const res = await axios.post(
                    'https://60a8d18120a6410017306479.mockapi.io/vue3todos/',
                    newTodo
                )
                todos.value.push(res.data)
            } catch (error) {
                console.log(error)
            }
        }

        return {
            todos,
            markCompleted,
            deleteTodo,
            addTodo,
        }
    },
}
</script>
