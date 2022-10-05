<script setup>
import { ref } from "vue";
import TagsInput from "./components/TagsInput.vue";

const tags = ref(["asdf", "wsdf", "esdf"]);
</script>

<template>
  <div class="p-4">
    <TagsInput
      v-model:tags="tags"
      v-slot="{ tag, removeTag, inputBindings, inputEventHandlers }"
    >
      <div class="tags-input">
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

        <input
          v-bind="inputBindings"
          v-on="inputEventHandlers"
          type="text"
          class="tags-input-text"
          placeholder="Add tag..."
        />
      </div>
    </TagsInput>
  </div>
</template>
