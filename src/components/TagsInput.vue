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
  if (newTag.value.length === 0 || props.tags.includes(newTag.value)) {
    return;
  }
  emit("update:tags", [...props.tags, newTag.value]);
  newTag.value = "";
};

const removeTag = (tag) => {
  emit(
    "update:tags",
    props.tags.filter((t) => t !== tag)
  );
};

const onInput = (e) => {
  newTag.value = e.target.value;
};
</script>

<template>
  <div class="tags-input">
    <slot
      name="tag"
      v-for="tag in tags"
      :tag="tag"
      :remove-tag="removeTag"
    ></slot>

    <slot name="input"
    :new-tag="newTag" 
    :on-input="onInput"
    :add-tag="addTag"
    :handle-tag-backspace="handleTagBackspace"
    ></slot>
  </div>
</template>
