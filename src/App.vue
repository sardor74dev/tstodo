<template>
  <AppHeader />

  <AppFilters
    :active-filter="activeFilter"
    @set-filter="setFilter"
  />

  <main class="app-main">
    <AppTodoList
      :todos="filteredTodos"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />

    <AppAddTodo @add-todo="addTodo" />
  </main>

  <AppFooter :stats="stats" />
</template>

<script lang="ts">
import { defineComponent } from "vue";
import AppHeader from "./components/AppHeader.vue";
import AppFilters from "./components/AppFilters.vue";
import AppTodoList from "./components/AppTodoList.vue";
import AppAddTodo from "./components/AppAddTodo.vue";
import AppFooter from "./components/AppFooter.vue";
import { Filter } from "@/types/Filter";
import Todo from "@/types/Todo";
import Stats from "@/types/Stats";

interface State {
  todos: Todo[];
  activeFilter: Filter;
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
      ],
      activeFilter: 'All'
    }
  },
  computed: {
    filteredTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos;
        case 'Done':
          return this.completedTodos;
        case 'All':
        default:
          return this.todos;
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.completedTodos.length
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => !todo.isDone);
    },
    completedTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => todo.isDone);
    },
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
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter;
    }
  }
})
</script>