<script setup lang="ts">
  import { ref } from 'vue'
  const count = ref(0);
</script>
<template>
  <div>
    <h1>counter</h1>
    {{ count }}
    <button @click="count++">늘려늘려</button>
  </div>
</template>