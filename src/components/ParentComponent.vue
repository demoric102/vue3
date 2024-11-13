<template>
  <div>
    <h3>Parent:</h3>
    <p>bool: {{ data.bool }}</p>
    <p>text: {{ data.text }}</p>
    <ChildComponent :data="data" @update="updateData" />
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import ChildComponent from './ChildComponent.vue';

// Parent data object
const data = reactive({
  bool: true,
  text: 'asdasd'
});

// Method to handle updates from the child component
function updateData(newData) {
  data.bool = newData.bool;
  data.text = newData.text;
}
</script>