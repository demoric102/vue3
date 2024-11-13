<template>
  <div>
    <textarea v-model="html" placeholder="Enter HTML code"></textarea>
    <textarea v-model="lessCode" placeholder="Enter LESS code"></textarea>
    <div v-html="compiledHtml" class="preview"></div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
import less from 'less';

const html = ref('<p>Example HTML</p>');
const lessCode = ref('p { color: red; }');
const compiledHtml = ref(html.value);
const compiledCss = ref('');

// Watch for changes in LESS code and compile it
watch(lessCode, (newCode) => {
  less.render(newCode, (err, output) => {
    if (err) {
      console.error('Error compiling LESS:', err);
    } else {
      compiledCss.value = output.css; // Store the compiled CSS
      applyStyles(compiledCss.value); // Apply the CSS to the document head
    }
  });
});

// Watch for changes in HTML code and update the preview
watch(html, (newHtml) => {
  compiledHtml.value = newHtml; // Update HTML preview
});

// Function to dynamically inject styles into the document head
function applyStyles(css) {
  let styleTag = document.getElementById('dynamic-styles');
  if (!styleTag) {
    styleTag = document.createElement('style');
    styleTag.id = 'dynamic-styles';
    document.head.appendChild(styleTag);
  }
  styleTag.innerHTML = css;
}
</script>

<style scoped>
textarea {
  display: block;
  width: 100%;
  margin-bottom: 10px;
  height: 100px;
}

.preview {
  border: 1px solid #ccc;
  padding: 10px;
}
</style>