<script setup>
import { RouterLink } from "vue-router";
</script>

<template>
  <header class="mb-2">
    <nav class="flex items-center justify-between p-5 bg-slate-100">
      <div class="flex items-center gap-2">
        <img src="../assets/logo.svg" alt="vue logo" width="50" />
        <h1>Vue Todos</h1>
      </div>
      <ul class="flex gap-5">
        <RouterLink
          to="/"
          active-class="border-b border-slate-300"
          class="px-2 py-1 transition-all hover:scale-105"
          >Home</RouterLink
        >
        <RouterLink
          to="/about"
          class="px-2 py-1 transition-all hover:scale-105"
          active-class="border-b border-slate-300"
          >About</RouterLink
        >
      </ul>
    </nav>
  </header>
</template>

<style lang="scss" scoped></style>
