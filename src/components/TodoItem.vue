<script setup>
const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <div class="w-3/4 p-1 mx-auto mb-2 font-bold text-center border shadow-lg">
    <h1>{{ todo.todo }}</h1>
  </div>
</template>
