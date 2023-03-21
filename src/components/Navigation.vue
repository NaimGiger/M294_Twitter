<script setup>
import { useAuth } from '../api/auth';
import IconHome from '../components/icons/IconHome.vue';
import IconLogin from '../components/icons/IconLogin.vue';

const { isLoggedIn, logout } = useAuth()
</script>

<template>
    <nav class="nav">
        <RouterLink to="/">
            <IconHome />
            Stream
        </RouterLink>
        <RouterLink to="/login" v-if="!isLoggedIn">
            <IconLogin />
            Login
        </RouterLink>
        <a href="#" class="logout-link" v-if="isLoggedIn" @click="logout()">
            <IconLogin />
            Logout
        </a>
    </nav>
</template>