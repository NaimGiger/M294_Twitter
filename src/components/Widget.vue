<script setup>
defineProps(['title'])
</script>

<template>
    <section class="widget">
        <h2 class="widget__heading">
            {{ title }}
        </h2>

        <slot />
    </section>
</template>