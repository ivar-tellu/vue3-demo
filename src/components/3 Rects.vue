<template>
    <div>
        <Rectangle :width="10" :height="10" color="green" />
        <Rectangle :width="20" :height="10" color="red" />
        <Rectangle :width="13" :height="5" color="blue" />
    </div>
</template>

<script setup lang="ts">
// Just import it, don't need to put it in a "components" array.
import Rectangle from './Rectangle.vue';
</script>