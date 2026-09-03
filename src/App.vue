<template>
  <AppHeader />

  <AppFilters />

  <main class="app-main">
    <AppTodoList
      :todos="todos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />

    <AppAddTodo @add-todo="addTodo" />
  </main>

  <AppFooter />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";
import Todo from "@/types/Todo";

interface State {
  todos: Todo[];
}

export default defineComponent({
  name: "App",
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
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
    addTodo(todo: Todo) {
      this.todos.push(todo);
    },
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