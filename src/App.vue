<script setup lang="ts">
import { ref } from 'vue';
import Christmas from './components/1 Christmas.vue';
import Example from './components/2 Example.vue';
import Rects from './components/3 Rects.vue';
import Slotted from './components/4 Slotted.vue';
import DisabledButton from './components/5 Disabled button.vue';

const showSimple = ref(false);
const showExample1 = ref(false);
const showRects = ref(false);
const showSlotted = ref(false);
const showDisabledButton = ref(false);
</script>

<template>
  <div class="controls">
    <label>show #1<input type="checkbox" v-model="showSimple"></label>
    <label>show #2<input type="checkbox" v-model="showExample1"></label>
    <label>show rects<input type="checkbox" v-model="showRects"></label>
    <label v-if="false">show slots<input type="checkbox" v-model="showSlotted"></label>
    <label v-if="false">show attribute<input type="checkbox" v-model="showDisabledButton"></label>
  </div>

  <!-- Components are used without putting them into a "components:" array. -->
  <Christmas v-if="showSimple" />
  <Example v-if=showExample1 :emojis="['🐕', '🐻', '🐊', '🐻‍❄️', '🐼']" />
  <Rects v-if="showRects" />
  <Slotted v-if="showSlotted">
    <template #slot><div>&lt;div&gt; inside the slot</div></template>
  </Slotted>
  <DisabledButton v-if="showDisabledButton" />
</template>

<style scoped>
.controls {
  left: 0;
  top: 0;
  position: fixed;
}
.controls label {
  display: block;
}
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
