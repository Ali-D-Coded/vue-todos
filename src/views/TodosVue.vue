<script setup>
import { ref, watch } from "vue";
import TodoCreator from "../components/TodoCreator.vue";
import { uid } from "uid";
import TodoItem from "../components/TodoItem.vue";
import { Icon } from "@iconify/vue";
const todoList = ref([]);

watch(todoList, () => setItemsToLocalStorage(), { deep: true });

const fetchTodoList = () => {
  const savedTodoList = JSON.parse(localStorage.getItem("todoList"));
  console.log(savedTodoList);
  if (savedTodoList.length > 0) {
    todoList.value = savedTodoList;
  }
};
fetchTodoList();

function setItemsToLocalStorage() {
  localStorage.setItem("todoList", JSON.stringify(todoList.value));
}

const createTodo = (todo) => {
  todoList.value.push({
    id: uid(),
    todo: todo,
    isEditing: false,
    isCompleted: false,
  });
};

const toggleComplete = (todoPos) => {
  todoList.value[todoPos].isCompleted = !todoList.value[todoPos].isCompleted;
};
const toggleEdit = (todoPos) => {
  todoList.value[todoPos].isEditing = !todoList.value[todoPos].isEditing;
};
const updateTodo = (todo, todoPos) => {
  console.log(todo, todoPos);
  todoList.value[todoPos].todo = todo;
  todoList.value[todoPos].isEditing = false;
};
const deleteTodo = (todoId) => {
  todoList.value = todoList.value.filter((todo) => todo.id !== todoId);
};
</script>

<template>
  <main>
    <h1 class="text-2xl font-bold text-center">Create Todo</h1>
    <TodoCreator @create-todo="createTodo" class="mb-10" />

    <ul v-if="todoList.length > 0">
      <TodoItem
        v-for="(todo, i) in todoList"
        :todo="todo"
        :index="i"
        @toggle-complete="toggleComplete"
        @toggle-edit="toggleEdit"
        @update-todo="updateTodo"
        @delete-todo="deleteTodo"
        v-bind:key="todo.id"
      />
    </ul>

    <p
      class="flex items-center justify-center w-3/4 mx-auto text-center"
      v-else
    >
      <Icon icon="ph:warning-fill" color="#fffc46" width="30" />
      <span> You have todos to complete! Add one! </span>
    </p>
  </main>
</template>
