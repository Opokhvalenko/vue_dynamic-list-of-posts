<script>
import { createComment } from "@/api/comments";
import InputField from "./InputField.vue";
import TextAreaField from "./TextAreaField.vue";
import Message from "./Message.vue";

export default {
  name: "AddComment",
  components: {
    InputField,
    TextAreaField,
    Message,
  },
  emits: ["cancel", "updateCommentsList"],
  props: {
    postId: Number,
  },
  data() {
    return {
      newAuthorName: "",
      newAuthorEmail: "",
      newCommentText: "",
      hasErrorText: false,
      hasErrorName: false,
      hasErrorEmail: false,
      isLoading: false,
      errorMessage: "",
    };
  },
methods: {
  createNewComment() {
    this.errorMessage = "";
    if (!this.validation()) {
      return;
    }

    const newData = {
      body: this.newCommentText,
      email: this.newAuthorEmail,
      name: this.newAuthorName, // 🔧 тут була помилка
      postId: this.postId,
    };

    this.isLoading = true;
    createComment(newData)
      .then(({ data }) => {
        this.newCommentText = "";
        this.newAuthorName = "";
        this.newAuthorEmail = "";
        this.$emit("updateCommentsList", data);
      })
      .catch((error) => {console.error("Error creating comment:", error);
          this.errorMessage = "Failed to add comment. Please try again.";})
      .finally(() => {
        this.isLoading = false;
      });
  },

  cancel() {
    this.$emit("cancel");
  },

  validation() {
    this.hasErrorName = !this.newAuthorName.trim();
    this.hasErrorEmail = !this.newAuthorEmail.trim();
    this.hasErrorText = !this.newCommentText.trim();

    return !(this.hasErrorName || this.hasErrorEmail || this.hasErrorText);
  },
},
};
</script>

<template>
  <form @submit.prevent="createNewComment">
    <InputField
      title="Author Name"
      v-model.trim="newAuthorName"
      :hasError="hasErrorName"
      name="authorName"
      placeholder="Name Surname"
      errorText="Name is required"
      @removeErr="hasErrorName = false"
    />

    <InputField
      title="Author Email"
      v-model.trim="newAuthorEmail"
      :hasError="hasErrorEmail"
      name="authorEmail"
      placeholder="Your Email"
      errorText="Email is required"
      @removeErr="hasErrorEmail = false"
    />

    <TextAreaField
      title="Write Comment Body"
      v-model.trim="newCommentText"
      :hasError="hasErrorText"
      name="commentText"
      placeholder="Comment"
      errorText="Body is required"
      @removeErr="hasErrorText = false"
    />

    <div class="field is-grouped">
      <div class="control">
        <button
          type="submit"
          class="button is-link"
          :class="{ 'is-loading': isLoading }"
        >
          Save
        </button>
      </div>
      <div class="control">
        <button
          @click="cancel"
          type="reset"
          class="button is-link is-light"
          :disabled="isLoading"
        >
          Cancel
        </button>
      </div>
    </div>
  </form>
</template>