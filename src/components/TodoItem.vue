<script setup>
import { Icon } from "@iconify/vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});
defineEmits(["toggle-complete", "toggle-edit", "update-todo", "delete-todo"]);
</script>

<template>
  <div
    class="flex items-center justify-between w-3/4 gap-5 px-2 py-3 mx-auto mb-2 font-bold text-center border shadow-lg bg-slate-100"
  >
    <div class="flex items-center gap-5">
      <input
        type="checkbox"
        :checked="todo.isCompleted"
        class="border outline-1"
        @input="$emit('toggle-complete', index)"
      />
      <div>
        <input
          v-if="todo.isEditing"
          type="text"
          :value="todo.todo"
          @keyup.enter="$emit('update-todo', $event.target.value, index)"
        />
        <span :class="{ ' line-through': todo.isCompleted }" v-else>{{
          todo.todo
        }}</span>
      </div>
    </div>
    <div class="flex gap-2">
      <!-- <Icon /> -->
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        color="#4d8e23"
        width="30"
        @click="$emit('toggle-edit', index)"
      />
      <Icon
        @click="$emit('toggle-edit', index)"
        v-else
        icon="ph:pencil-fill"
        color="#4d8e23"
        width="30"
      />
      <Icon
        icon="ph:trash"
        color="#f95e5e"
        width="30"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </div>
</template>
