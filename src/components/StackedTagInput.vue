<script setup>
import { ref } from "vue";
import TagsInput from "./TagsInput.vue";

const tags = ref(["asdf", "wsdf", "esdf"]);
</script>

<template>
  <TagsInput
    v-model:tags="tags"
    v-slot="{ tag, removeTag, inputBindings, inputEventHandlers }"
  >
    <div class="p-4 border rounded flex flex-col gap-4">
      <input
        v-bind="inputBindings"
        v-on="inputEventHandlers"
        type="text"
        class="tags-input-text"
        placeholder="Add tag..."
      />

      <div class="flex flex-wrap gap-2">
        <span
          v-for="tag in tags"
          class="tags-input-tag bg-purple-200 text-purple-900"
        >
          <span>{{ tag }}</span>
          <button
            type="button"
            @click="removeTag(tag)"
            class="tags-input-remove"
          >
            &times;
          </button>
        </span>
      </div>
    </div>
  </TagsInput>
</template>
