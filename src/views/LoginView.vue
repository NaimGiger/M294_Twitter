<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'
import { loginUser } from '../api/requests.js';

const email = ref('')
const password = ref('')
const router = useRouter()

const errors = ref({
  email: '',
  password: ''
})

async function login() {
  try {
    await loginUser(email.value, password.value)
    console.log('login successful')
    await router.push('/')
  } catch (exception) {
    console.error(exception)
    errors.value = exception.errors
  }
}
</script>

<template>
  <div class="login">
    <section class="login-wrapper">
      <form action="#" class="login-form" autocomplete="off" novalidate @submit.prevent="login">
        <div class="form-group">
          <label class="form-label" for="email">E-Mail</label>
          <input class="form-input" type="email" id="email" v-model="email"/>
          <div class="form-error" v-if="errors.email.length">
            {{ errors.email }}
          </div>
        </div>
        <div class="form-group">
          <label class="form-label" for="password">Passwort</label>
          <input class="form-input" type="password" id="password" v-model="password" />
          <div class="form-error" v-if="errors.password.length">
            {{ errors.password }}
          </div>
        </div>
        <div class="form-group">
          <button class="btn btn--primary btn--block" :disabled="email.length <1 || password.length < 1">
            Login
          </button>
        </div>
      </form>
    </section>
  </div>
</template>

