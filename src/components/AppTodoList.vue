<template>
    <ul class="todo-list">
        <AppTodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import Todo from "@/types/Todo";

interface State {
    todos: Todo[];
}

export default defineComponent({
    name: "AppTodoList",
    components: {
        AppTodoItem
    },
    data(): State {
        return {
            todos: [
                { id: 1, text: "Learn the basics of Vue", isDone: true },
                { id: 2, text: "Learn the basics of Typescript", isDone: false },
                { id: 3, text: "Subscribe to the channel", isDone: false },
            ]
        }
    }
})
</script>