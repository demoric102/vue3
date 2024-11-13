<template>
  <div>
    <h1>Vue 3 Project</h1>
    <!-- Task 1 -->
    <ParentComponent />
    <hr />
    <!-- Task 2 -->
    <CodeEditor />
  </div>
</template>

<script setup>
import ParentComponent from './components/ParentComponent.vue';
import CodeEditor from './components/CodeEditor.vue';
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 20px;
}
hr {
  margin: 40px 0;
}
</style>