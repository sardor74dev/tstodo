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
import { PropType, defineComponent } from "vue";
import AppTodoItem from "./AppTodoItem.vue";
import Todo from "@/types/Todo";

export default defineComponent({
    name: "AppTodoList",
    components: {
        AppTodoItem
    },
    props: {
        todos: {
            type: Array as PropType<Todo[]>
        }
    },
    methods: {
        toggleTodo(id: number) {
            this.$emit('toggle-todo', id);
        },
        removeTodo(id: number) {
            this.$emit('remove-todo', id);
        }
    },
    emits: {
        'toggle-todo': (id: number) => true,
        'remove-todo': (id: number) => true
    }
})
</script>