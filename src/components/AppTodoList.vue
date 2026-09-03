<template>
    <ul class="todo-list">
        <AppTodoItem
            v-for="todo in todos" 
            :key="todo.id"
            :todo="todo"
            @toggle-todo="toggleTodo"
            @remove-todo="removeTodo"
        />
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
    },
    methods: {
        toggleTodo(id: number) {
            const target = this.todos.find((todo: Todo) => todo.id === id);
            if (target) {
                target.isDone = !target.isDone;
            }
        },
        removeTodo(id: number) {
            this.todos = this.todos.filter((todo: Todo) => todo.id !== id);
        }
    }
})
</script>