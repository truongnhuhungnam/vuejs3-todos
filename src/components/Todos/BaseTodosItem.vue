<template>
    <li class="flex justify-between py-2">
        <label>
            <input
                type="checkbox"
                class="form-checkbox rounded text-pink-500 mr-2"
                :checked="todoProps.completed"
                @change="markTodoCompleted"
            />
            <span :class="todoProps.completed ? 'line-through' : ''">
                {{ todoProps.title }}
            </span>
        </label>
        <button
            class="
                bg-purple-400
                text-white
                px-4
                py-1
                hover:opacity-50
                transition-all
                border border-purple-400
            "
            @click="deleteTodo"
        >
            Delete
        </button>
    </li>
</template>

<script>
// import { ref } from 'vue'
export default {
    props: ['todoProps'],
    setup(props, context) {
        const markTodoCompleted = () => {
            context.emit('todo-completed', props.todoProps.id)
        }

        const deleteTodo = () => {
            context.emit('todo-delete', props.todoProps.id)
        }

        return { markTodoCompleted, deleteTodo }
    },
}
</script>
