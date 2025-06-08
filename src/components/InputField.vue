<script>
export default {
  name: "InputField",
  props: {
    name: String,
    placeholder: String,
    errorText: String,
    modelValue: String,
    hasError: Boolean,
    title: String,
  },
  emits: ["update:modelValue", 'removeErr'],
};
</script>

<template>
  <div class="field" data-cy="NameField">
    <label
      class="label input-field__label"
      :for="`comment-author-name-${name}`"
    >
      {{ title }}
    </label>
    <div class="control has-icons-left has-icons-right">
      <input
        type="text"
        :name="name"
        :id="`comment-author-name-${name}`"
        :placeholder="placeholder"
        class="input"
        :class="{ 'is-danger': hasError }"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value); $emit('removeErr')"
        
      />
      <span class="icon is-small is-left">
        <i
          class="fas"
          :class="{
            'fa-user': !name.toLowerCase().includes('email'),
            'fa-envelope': name.toLowerCase().includes('email'),
          }"
        ></i>
      </span>

      <span
        class="icon is-small is-right has-text-danger"
        data-cy="ErrorIcon"
        v-if="hasError"
      >
        <i class="fas fa-exclamation-triangle"></i>
      </span>
    </div>

    <p class="help is-danger" data-cy="ErrorMessage" v-if="hasError">
      {{ errorText }}
    </p>
  </div>
</template>

<style>
.input-field__label {
  text-transform: capitalize;
}
</style>