<script setup>
import { onMounted, ref } from 'vue';
import { fetchTopUsers } from '../api/requests';
import Widget from './Widget.vue';

const topUsers = ref([])
const loading = ref(true)

onMounted(async () => {
    try {
        const stream = await fetchTopUsers()
        topUsers.value = stream
    } catch (error) {
        console.error(error)
    } finally {
        loading.value = false
    }
});
</script>

<template>
    <Widget title="Top User">
        <ul class="content-list">
            <p v-if="loading" class="content-list__item">
                loading...
            </p>
            <li class="content-list__item" v-for="user in topUsers">
                <a href="#">
                    <span class="content-list__meta">
                        {{ user.tweets_count }}
                    </span>
                    <span class="content-list__text">
                        {{ user.name }}
                    </span>
                </a>
            </li>
        </ul>
    </Widget>
</template>