<script setup>
import { computed, ref } from 'vue';
import { createTweet } from '../api/requests';

const emit = defineEmits(['posted'])

const text = ref("")
const textLength = computed(() => text.value.length)
function submit() {
    createTweet(text.value)
    emit('posted')
}
</script>

<template>
    <form class="composer">
        <label class="composer__prompt">Was geht?</label>
        <textarea maxlength="160" class="composer__textarea" placeholder="Verfasse einen Tweet..." v-model="text"/>
        <div class="composer__actions">
            <div class="composer__stats stats">
                <span class="stats__counter">{{ textLength }}</span>
                <span class="stats__max">/ 160</span>
            </div>
            <button :disabled="textLength < 5" class="btn btn--primary" @click="submit()">
                Tweet veröffentlichen
            </button>
        </div>
    </form>
</template>
