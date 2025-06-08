<script>
export default {
  name: "WriteCommentBtn",
  emits: ["click"],
};
</script>

<template>
  <button 
  type="button" 
  class="button is-link" 
  @click="$emit('click')"
  aria-label="Write a comment"
  >
    <slot>Write a comment</slot>
    </button>
</template>