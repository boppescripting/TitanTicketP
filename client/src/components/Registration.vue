<template>
  <div>
    <h1>Register</h1>
    <label for="email">Email Address</label>
    <input type="email" name="email" v-model="email">
    <br>
    <label for="password">Password</label>
    <input type="password" name="password" v-model="password">
    <br>
    <button @click="register">Register</button>
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    async register () {
      const res = await AuthenticationService.register({
        email: this.email,
        password: this.password
      })
      console.log(res.data)
    }
  }
}
</script>

<style scoped>
</style>
