<template>
    <li class="todo-item" :class="{'todo-item--done' : todo.isDone}" @click="toggleTodo">
        <div class="todo-item__status">
            <i class="bi bi-check2"></i>
        </div>
        <span class="todo-item__text">{{ todo.text }}</span>
        <button class="todo-item__remove-button">
            <i class="bi bi-trash3"></i>
        </button>
    </li>
</template>

<script lang="ts">
import Todo from "@/types/Todo";
import { PropType, defineComponent } from "vue";

export default defineComponent({
    name: "AppTodoItem",
    props: {
        todo: {
            type: Object as PropType<Todo>,
            required: true
        }
    },
    methods: {
        toggleTodo() {
            this.$emit('toggle-todo', this.todo.id);
        }
    },
    emits: {
        'toggle-todo': (id: number) => true
    }
})
</script>