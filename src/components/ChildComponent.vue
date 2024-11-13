<template>
  <div>
    <h4>Child:</h4>
    <p>bool: {{ data.bool }}</p>
    <p>text: {{ data.text }}</p>
    <button @click="toggleBool">Change Bool</button>
    <input v-model="data.text" @input="updateParent" />
  </div>
</template>

<script setup>
import { toRefs } from 'vue';

const props = defineProps(['data']);
const emit = defineEmits();

// Destructure reactive data for easier reactivity
const { bool, text } = toRefs(props.data);

// Method to toggle the bool value
function toggleBool() {
  emit('update', { bool: !bool.value, text: text.value });
}

// Emit the updated text value to the parent
function updateParent() {
  emit('update', { bool: bool.value, text: text.value });
}
</script>