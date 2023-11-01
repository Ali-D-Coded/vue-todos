<script setup>
import { ref } from "vue";
import TodoCreator from "../components/TodoCreator.vue";
import { uid } from "uid";
import TodoItem from "../components/TodoItem.vue";
const todoList = ref([]);

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
</script>

<template>
  <main>
    <h1 class="text-2xl font-bold text-center">Crea te Todo</h1>
    <TodoCreator @create-todo="createTodo" class="mb-10" />
    <TodoItem v-for="todo in todoList" :todo="todo" v-bind:key="todo.id" />
  </main>
</template>
