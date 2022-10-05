<script setup>
import { ref } from "vue";

const props = defineProps(["tags"]);
const emit = defineEmits(["update:tags"]);

const newTag = ref("");

const handleTagBackspace = () => {
  if (newTag.value.length === 0) {
    emit("update:tags", props.tags.slice(0, -1));
  }
};

const addTag = () => {
  if (newTag.value.length === 0 || props.tags.includes(newTag.value)) {
    return;
  }
  emit("update:tags", [...props.tags, newTag.value]);
  newTag.value = "";
  console.log(newTag.value);
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

const onKeyDown = (e) => {
  if (e.keyCode === 8) {
    handleTagBackspace();
  }

  if (e.keyCode === 13) {
    e.preventDefault();
    addTag();
  }
};
</script>

<template>
  <div class="tags-input">
    <slot
        :tags="tags"
        :remove-tag="removeTag"
        :input-bindings="{ value: newTag }"
        :input-event-handlers="{
          input: onInput,
          keydown: onKeyDown,
        }"
    ></slot>
  </div>
</template>
