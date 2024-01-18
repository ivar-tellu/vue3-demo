This example shows usage of Vue 3 refs.
The ref'd value becomes a wrapper object.

<template>
    <!-- No .value when accessing a ref in a template (they are automatically unwrapped). -->
    <label>is it christmas?<input type="checkbox" v-model="isItChristmas" /></label>

    <div v-if="isItChristmas">
        <div class="santa" :shake="santaShake">
            🎅
        </div>
        <div class="speech">
            {{ santaSpeech }}
        </div>

        <button @click="gotcha">it is not Christmas</button>
        <button v-if="santaShake" @click="santaShake = null; santaSpeech = 'ok :-)'">calm down</button>
    </div>
</template>

<script setup lang="ts">
// New in Vue 3: Have to import ref, computed, onMounted, etc.
import { ref } from 'vue';

// ref() is the default way to create reactive state, much like putting it in 'data: {}' in Vue 2.
// reactive() can also be used, but it has a bunch of limitations. ref() calls reactive().
// Always use ref() unless you have a VERY good reason not to.
// ref() will wrap the object, and the type of the object in this case be Ref<boolean>.
const isItChristmas = ref(false);

const gotchaBool = ref(false);
function gotcha() {
    // Because the variable is a wrapper object, it is not suficcient to check for the wrapper's truthiness.
    alert(`Bool value: ${gotchaBool.value}\nWrapper value: ${gotchaBool}\nWrapper truthiness: ${!!gotchaBool}`);
    // Conclusion: ALWAYS use .value in <script>.

    santaSpeech.value = 'Christmas is R̶̳͆U̴̹̎I̷͎͘N̵̲̓E̴̹͂D̸͓͑';
    santaShake.value = true;
}

const santaSpeech = ref('- It is Christmas. Hello.');
const santaShake = ref<Boolean | null>(null);
</script>

<style>
.santa {
    font-size: 152px;
    color: white;
    display: inline-block;
    transition: 3s;
}
.santa[shake] {
    animation: 100ms infinite santa-shake;
}
@keyframes santa-shake {
    0% {
        transform: translate(5px, 5px);
    }
    20% {
        transform: rotateZ('18deg');
        filter: blur(5px);
    }
    40% {
        transform: translate(-8px, -7px);
    }
    60% {
        transform: rotateZ('-10deg');
    }
    80% {
        transform: rotateZ('-20deg') translate(10px, 0px);
        filter: brightness(5);
    }
}
.santa:hover {
    filter: hue-rotate(360deg);
}
.speech {
    text-align: center;
}
</style>