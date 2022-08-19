<script setup>
import 'agnostic-vue/dist/common.min.css'
import "agnostic-vue/dist/index.css";

import TodoList from './components/TodoList.vue';
</script>

<template>
  <TodoList />
</template>

<style scoped>
.root {
  font-family: var(--agnostic-font-family-body);
  font-size: var(--agnostic-body);
  color: var(--agnostic-font-color);
  line-height: 1.5;
}




</style>
