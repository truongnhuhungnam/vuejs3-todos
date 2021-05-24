<template>
    <div>
        <form @submit.prevent="addTodo" class="w-full">
            <input
                type="text"
                class="form-input mr-2 w-1/3"
                placeholder="Add Task"
                v-model="title"
            />
            <input
                type="submit"
                value="Add Todo"
                class="
                    bg-purple-400
                    text-white
                    px-4
                    py-2
                    hover:opacity-50
                    transition-all
                    border border-purple-400
                    cursor-pointer
                "
            />
        </form>
    </div>
</template>

<script>
import { ref } from 'vue'
export default {
    setup(props, context) {
        const title = ref('')
        const addTodo = () => {
            const newTodo = {
                title: title.value,
                completed: false,
            }
            context.emit('todo-add', newTodo)

            title.value = ' '
        }
        return { title, addTodo }
    },
}
</script>
