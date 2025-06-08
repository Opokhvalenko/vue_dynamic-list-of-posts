<script>
export default {
  name: "TextAreaField",
  props: {
    modelValue: {
    type: String,
    default: ''
  },
    name: String,
    placeholder: String,
    title: String,
    errorText: String,
    hasError: Boolean,
  },
  emits: ["update:modelValue", "removeErr"],
};
</script>

<template>
  <div class="field" data-cy="BodyField">
    <label class="label textarea-field__label" :for="`comment-${name}`">
      {{ title }}
    </label>
    <div class="control">
      <textarea
        :id="`comment-${name}`"
        :name="name"
        :placeholder="placeholder"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value); $emit('removeErr')"
        :class="{ 'is-danger': hasError }"
        class="textarea"
        autocomplete="off"
      ></textarea>
    </div>

    <p v-if="hasError" class="help is-danger" data-cy="ErrorMessage">
      {{ errorText }}
    </p>
  </div>
</template>

<style>
.textarea-field__label {
  text-transform: capitalize;
}
</style>