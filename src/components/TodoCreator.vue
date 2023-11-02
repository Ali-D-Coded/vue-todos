<script setup>
import { reactive, ref } from "vue";

const emit = defineEmits(["create-todo"]);

const todoState = reactive({
  todo: "",
  isInvalid: false,
  isEditable: false,
  errMsg: "",
});

const emitTodo = () => {
  if (todoState.todo !== "") {
    emit("create-todo", todoState.todo);
    todoState.todo = "";
    todoState.isInvalid = false;
    todoState.errMsg = "";
    return;
  }
  todoState.isInvalid = true;
  todoState.errMsg = "Nothing in the todo";
  console.log({ todoState });
};
</script>

<template>
  <div class="flex flex-col items-center my-5">
    <div class="flex w-3/4 bg-slate-100">
      <input
        type="text"
        v-model="todoState.todo"
        class="flex-1 border focus:outline-none"
        :class="{ 'outline outline-red-800': todoState.isInvalid }"
      />

      <button class="w-32 h-10" @click="emitTodo()">Create</button>
    </div>
    <p v-show="todoState.isInvalid">
      {{ todoState.errMsg }}
    </p>
  </div>
</template>
