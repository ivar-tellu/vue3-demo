<template>
    <div>
        <slot name="slot" />
    </div>
</template>

<style scoped>
/* This is not applied to anything inside the slot. */
div {
    background-color: yellow !important;
}
/* If we absolutely must apply style to something iside the slot, we need :slotted. */
:slotted(div) {
    background-color: blue;
}
</style>

More info: https://vuejs.org/api/sfc-css-features.html#slotted-selectors