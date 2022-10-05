<script setup>
import { ref } from "vue";
import TagsInput from "./components/TagsInput.vue";

const tags = ref(["asdf", "wsdf", "esdf"]);
</script>

<template>
  <div class="p-4">
    <TagsInput v-model:tags="tags">
      <template #tag="{ tag, removeTag }">
        <span class="tags-input-tag bg-purple-200 text-purple-900">
          <span>{{ tag }}</span>
          <button
            type="button"
            @click="removeTag(tag)"
            class="tags-input-remove"
          >
            &times;
          </button>
        </span>
      </template>

      <template #input="{ newTag, onInput, handleTagBackspace, addTag }">
        <input
        type="text"
        class="tags-input-text"
        placeholder="Add tag..."
        @keydown.backspace="handleTagBackspace"
        @keydown.enter.prevent="addTag"

        :value="newTag"
        @input="onInput"
        />
      </template>
    </TagsInput>
  </div>
</template>
