<script>
export default {
  name: "CommentForm",
  data() {
    return {
      name: "",
      email: "",
      comment: "",
      hasErrorName: false,
      hasErrorComment: false,
    };
  },
  methods: {
    submitComment() {
      this.hasErrorName = !this.name.trim();
      this.hasErrorComment = !this.comment.trim();

      if (this.hasErrorName || this.hasErrorComment) {
        return;
      }

      const newComment = {
        name: this.name.trim(),
        email: this.email.trim(),
        body: this.comment.trim(),
      };

      this.$emit("submit", newComment);

      // Скидання полів
      this.name = "";
      this.email = "";
      this.comment = "";
      this.hasErrorName = false;
      this.hasErrorComment = false;
    },
    removeNameError() {
      this.hasErrorName = false;
    },
    removeCommentError() {
      this.hasErrorComment = false;
    },
  },
};
</script>

<template>
  <div>
    <input
      class="input"
      type="text"
      placeholder="Your name"
      v-model="name"
      @input="removeNameError"
      :class="{ 'is-danger': hasErrorName }"
    />
    <p v-if="hasErrorName" class="help is-danger">Name is required</p>

    <input
      class="input mt-2"
      type="email"
      placeholder="Your email (optional)"
      v-model="email"
    />

    <textarea
      class="textarea mt-2"
      placeholder="Write your comment..."
      v-model="comment"
      @input="removeCommentError"
      :class="{ 'is-danger': hasErrorComment }"
    ></textarea>
    <p v-if="hasErrorComment" class="help is-danger">Comment cannot be empty</p>

    <button class="button is-primary mt-3" @click="submitComment">
      Send
    </button>
  </div>
</template>

<style scoped>
.input,
.textarea {
  width: 100%;
}
</style>