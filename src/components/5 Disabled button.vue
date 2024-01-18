<template>
    <button :disabled="true">button[disabled="true"]</button>
    <button :disabled="false">button[disabled="false"]</button>
    <button disabled>button[disabled]</button>
    <button :disabled="isFalse">button[disabled="false"]</button>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const isFalse = ref(false);
</script>