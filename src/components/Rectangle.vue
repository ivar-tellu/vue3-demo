<template>
    <div class="rect" :style="computedStyle">
        {{ area }}
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const { width, height, color, } = defineProps({
    width: { type: Number, required: true },
    height: { type: Number, required: true },
    color: { type: String, required: true },
});

const computedStyle = computed(() => {
    return {
        width: `${width}em`,
        height: `${height}em`,
        lineHeight: `calc(${height}em - 10px)`,
        borderColor: color,
    };
});

const area = computed(() => `${width * height}em²`);
</script>

<style scoped>
.rect {
    margin: 1px;
    border: 5px solid gray;
    font-size: 20px;
    text-align: center;
}
.rect:hover {
    border-style: dotted;
    background-color: #333;
}
</style>