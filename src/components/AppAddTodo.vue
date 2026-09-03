<template>
    <section class="add-todo">
        <form
            v-if="isFormVisible"
            class="add-todo__form"
            @submit.prevent="addTodo"
        >
            <button class="close-button" type="button" @click="hideForm">
                <i class="bi bi-x"></i>
            </button>
            <div class="text-input text-input--focus">
                <input class="input" v-model="todoText" />
            </div>
            <button class="button button--filled">Add task</button>
        </form>
        <button v-else @click="showForm" class="add-todo__show-form-button">
            <i class="bi bi-plus-lg"></i>
        </button>
    </section>
</template>

<script lang="ts">
import Todo from "@/types/Todo";
import { defineComponent } from "vue";

interface State {
    isFormVisible: boolean;
    todoText: string;
}

export default defineComponent({
    name: "AppAddTodo",
    data(): State {
        return {
            isFormVisible: false,
            todoText: ""
        }
    },
    methods: {
        showForm() {
            this.isFormVisible = true;
        },
        hideForm() {
            this.isFormVisible = false;
        },
        addTodo() {
            this.$emit('add-todo', {
                id: Date.now(),
                text: this.todoText,
                isDone: false
            })
            this.todoText = ""
        }
    },
    emits: {
        'add-todo': (todo: Todo) => todo
    }
})
</script>