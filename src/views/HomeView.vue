<script setup>
import { useAuth } from '../api/auth';
import { checkAuth, fetchStream } from '../api/requests.js';
import Composer from '../components/Composer.vue';
import LoginInfo from '../components/LoginInfo.vue';
import Tweet from '../components/Tweet.vue';

import { onMounted, ref } from 'vue';

const loading = ref(true)
const tweets = ref([])
const { isLoggedIn } = useAuth()

onMounted(async () => {
    // const response = await checkAuth()
    // console.log('checkAuth Resultat', response)
})

function loadStream() {
    onMounted(async () => {
        loading.value = true
        try {
            const stream = await fetchStream()
            tweets.value = await stream
        } catch (error) {
            console.error(error)
        } finally {
            loading.value = false
        }
        setTimeout(() => {
            loading.value = false
        }, 3000)
    })
}

loadStream()
</script>

<template>
    <LoginInfo v-if="!isLoggedIn" />
    <Composer v-if="isLoggedIn" @posted="loadStream()" />
    <section class="stream" v-if="!loading">
        <Tweet v-for="tweet in tweets" :user="tweet.user" :text="tweet.text" :created-at="tweet.createdAt" />
    </section>
    <div class="loading" v-if="loading">
        Lade Tweets...
    </div>
</template>
