<script setup>
import { ref } from "vue";
import TagsInput from "./components/TagsInput.vue";

const tags = ref(["asdf", "wsdf", "esdf"]);
</script>

<template>
  <div class="p-4">
    <TagsInput v-model:tags="tags">
      <template #tag="props">
        <span class="tags-input-tag">
          <span>{{ props.tag }}</span>
          <button type="button" @click="props.removeTag(props.tag)" class="tags-input-remove">
            &times;
          </button>
        </span>
      </template>
    </TagsInput>
  </div>
</template>
