<script setup>
import { ref } from "vue";

const props = defineProps(["tags"]);
const emit = defineEmits(["update:tags"]);

const newTag = ref("");

const handleTagBackspace = (e) => {
  if (newTag.value.length === 0) {
    emit("update:tags", props.tags.slice(0, -1));
  }
};

const addTag = (e) => {
    if (newTag.value.length === 0 || props.tags.includes(newTag.value)){
        return;
    }
    emit('update:tags', [...props.tags, newTag.value]);
    newTag.value = '';
};

const removeTag = (tag) => {
    emit('update:tags', props.tags.filter(t => t !== tag));
};
</script>

<template>
  <div class="tags-input">
    <span v-for="tag in tags" class="tags-input-tag">
      <span>{{ tag }}</span>
      <button type="button" @click="removeTag(tag)" class="tags-input-remove">
        &times;
      </button>
    </span>
    <input
      type="text"
      class="tags-input-text"
      placeholder="Add tag..."
      @keydown.backspace="handleTagBackspace"
      @keydown.enter.prevent="addTag"
      v-model="newTag"
    />
  </div>
</template>

<style>
    .tags-input {
        @apply border rounded p-2 flex flex-wrap gap-2;
    }
</style>