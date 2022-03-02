<script setup lang="ts">
import { computed, reactive, ref, watchEffect } from "vue";
import type { Input } from "@nordhealth/components";

// helper for demo purposes
function useField(initialValue = "") {
  const inputRef = ref<Input>();
  const value = ref(initialValue);
  const error = ref<string>();
  const valid = computed(() => !!value.value);

  // clear error whenever value is valid
  watchEffect(() => {
    if (valid.value) {
      error.value = undefined;
    }
  });

  return reactive({
    value,
    error,
    valid,
    focus: () => inputRef.value?.focus(),
    setRef: (el: Input) => {
      inputRef.value = el;
    },
  });
}

const username = useField();
const password = useField();

function handleSubmit() {
  if (username.valid && password.valid) {
    alert(`User: ${username.value}\nPassword: ${password.value}`);
  }

  if (!password.valid) {
    password.error = "Please enter a password";
    password.focus();
  }

  if (!username.valid) {
    username.error = "Please enter a username";
    username.focus();
  }
}
</script>

<template>
  <nord-card padding="l">
    <h2 slot="header">Sign in to Nord</h2>
    <form action="#" @submit.prevent="handleSubmit">
      <nord-stack>
        <nord-input
          label="Username"
          expand
          type="email"
          name="username"
          placeholder="user@example.com"
          :ref="username.setRef"
          :error="username.error"
          v-model="username.value"
        ></nord-input>

        <div class="password">
          <nord-input
            label="Password"
            expand
            type="password"
            name="password"
            placeholder="••••••••"
            :ref="password.setRef"
            :error="password.error"
            v-model="password.value"
          >
          </nord-input>
          <a href="#">Forgot password?</a>
        </div>

        <nord-button type="submit" expand variant="primary">
          Sign in
        </nord-button>
      </nord-stack>
    </form>
  </nord-card>

  <nord-card class="n-align-center">
    New to Nord? <a href="#">Create an account</a>.
  </nord-card>
</template>

<style scoped>
.password {
  position: relative;
}

.password a {
  text-decoration: none;
  font-size: var(--n-font-size-s);
  position: absolute;
  inset-block-start: 0;
  inset-inline-end: 0;
}
</style>
