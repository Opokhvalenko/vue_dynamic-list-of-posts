<script>
export default {
  name: "NeedToRegister",
  props: {
    modelValue: String, // Для v-model з Login.vue (значення 'name')
    errMessage: String, // Для відображення помилки, що передається з Login.vue
  },
  emits: ["update:modelValue", "onInput"], // Для двостороннього зв'язування і очищення помилки
};
</script>

<template>
  <div class="message is-warning">
    <div class="message-header">
      <p>Registration Needed</p>
    </div>
    <div class="message-body">
      <p>It looks like you don't have an account with this email. Please enter your name to register.</p>
      <div class="field mt-3">
        <label class="label" for="user-name">Name</label>
        <div class="control has-icons-left">
          <input
            type="text"
            id="user-name"
            name="name"
            class="input"
            placeholder="Enter your name"
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value); $emit('onInput')"
            :class="{ 'is-danger': errMessage }"
            required
          />
          <span class="icon is-small is-left">
            <i class="fas fa-user"></i>
          </span>
        </div>
        <p v-if="errMessage" class="help is-danger">{{ errMessage }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>