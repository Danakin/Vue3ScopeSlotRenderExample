<script setup>
  import { ref } from 'vue';
import TagsInput from './components/TagsInput.vue';

  const tags = ref([
    'asdf','wsdf','esdf'
  ]);
</script>

<template>
  <div class="p-4">
    <TagsInput v-model:tags="tags" />
  </div>
</template>
