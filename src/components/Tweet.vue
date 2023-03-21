<script setup>
import { formatDistance } from 'date-fns';

defineProps(['text', 'user', 'createdAt'])
</script>

<template>
    <div class="tweet">
        <div class="tweet__avatar">
            <img :src="`https://i.pravatar.cc/100?u=${user.id}`" alt="" />
        </div>
        <div class="tweet__content">
            <div class="tweet__header">
                <span class="tweet__author">
                    {{ user.name }}
                </span>
                <span class="tweet__timestamp">
                    {{ formatDistance(new Date(createdAt), new Date()) }}
                </span>
            </div>
            <div class="tweet__text">
                {{ text.substr(0, 80) }}
            </div>
        </div>
    </div>
</template>