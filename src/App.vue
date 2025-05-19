<script setup lang="ts">
import { ref } from 'vue';

const name = ref('');
const count = ref(0);
</script>

<template>
  <nord-input label="Your name" v-model="name"></nord-input>
  <p>{{ name }}</p>

  <nord-button variant="primary" @click="count++">
    Count: {{ count }}
  </nord-button>
</template>