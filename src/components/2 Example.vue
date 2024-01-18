<template>
    <div @wheel="scrollEmoji" class="emoji" :style="emojiParentStyle">
        <div v-for="(emoji, index) in emojis" :key="emoji" @click="rotateEmoji(36 * (index + 1))" class="emoji" :style="emojiStyle">
            {{ emoji }}
        </div>
    </div>

    <div>
        <ul>
            <li>{{ rotationDegrees }}°</li>
            <li>{{ completedRevolutions }} flips + {{ rotationDegrees % 360 }}°</li>
        </ul>
    </div>

</template>

<script setup lang="ts">
// New in Vue 3: Have to import ref, computed, onMounted, etc.
import { computed, onMounted, ref, type PropType } from 'vue';

// It can be a good idea to put logic in script files rather than cramming everything into the .vue file.
// Especially if it's logic that can be reused.

const rotationDegrees = ref(37);
// When accessing a ref in a script, you NEED to use .value. This is not needed in <template>
/*
rotationDegrees.toString() => '[object Object]'
rotationDegrees.value => 37
JSON.stringify(rotationDegrees) => '{"__v_isShallow":false,"__v_isRef":true,"_rawValue":37,"_value":37}'
JSON.stringify(rotationDegrees.value) => '37'
*/

const emojiParentStyle = computed(() => ({
    transform: `rotateZ(${rotationDegrees.value}deg)`
}));
const emojiStyle = computed(() => ({
    transform: `rotateZ(${-rotationDegrees.value}deg)`
}));
const completedRevolutions = computed(() => Math.floor(rotationDegrees.value / 360));

const { emojis } = defineProps({
    emojis: {
        type: Array as PropType<Array<string>>,
        required: true,
    },
});

onMounted(() => {
    // mounted() on the component has been changed into this imported function call with a callback.
});

const rotateEmoji = (degrees: number) => {
    // Need .value when accessing a ref's value in a script.
    const newDegrees = rotationDegrees.value + degrees;
    rotationDegrees.value = newDegrees;
};
const scrollEmoji = (event: WheelEvent) => {
    rotateEmoji(event.deltaY);
};
</script>

<style>
.emoji {
    user-select: none;
    font-size: 80px;
    transition: 600ms;
    transition-timing-function: ease-out;
}
</style>