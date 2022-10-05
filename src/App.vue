<script setup>
import { ref } from "vue";
import TagsInput from "./components/TagsInput.vue";

const tags = ref(["asdf", "wsdf", "esdf"]);
</script>

<template>
  <div class="p-4">
    <TagsInput v-model:tags="tags">
      <template #tag="{tag, removeTag}">
        <span class="tags-input-tag">
          <span>{{ tag }}</span>
          <button type="button" @click="removeTag(tag)" class="tags-input-remove">
            &times;
          </button>
        </span>
      </template>
    </TagsInput>
  </div>
</template>
