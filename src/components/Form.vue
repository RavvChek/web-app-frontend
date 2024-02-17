<template>
  <h2>LOGIN ACCOUNT</h2>
  <form>
    <label for="login"></label>
    <input name="login" type="text" placeholder="Login" v-model="login"/>
    <label for="password"></label>
    <input name="password" type="password" placeholder="Password" v-model="password"/>
    <br>
    <button v-on:click="onLogin">LOGIN</button>
    <button v-on:click="onRegister">REGISTER</button>
  </form>
</template>

<script>

import router from '@/router'

export default {
  name: 'FormView',
  components: {},
  data () {
    return {
      login: '',
      password: ''
    }
  },
  methods: {
    onLogin () {
      event.preventDefault()
      this.login = encodeURI(this.login.trim())
      this.password = encodeURI(this.password.trim())
      if (this.login === '' || this.password === '') {
        return
      }
      const formData = new FormData()
      formData.append('login', this.login.toString())
      formData.append('password', this.password.toString())
      fetch('/app/server/login', {
        method: 'POST',
        body: formData
      }).then(response => {
        if (response.ok) {
          router.push({
            path: '/start',
            params: { login: this.login }
          })
        }
      })
    },
    onRegister () {
      event.preventDefault()
      this.login = encodeURI(this.login.trim())
      this.password = encodeURI(this.password.trim())
      if (this.login === '' || this.password === '') {
        return
      }
      const formData = new FormData()
      formData.append('login', this.login.toString())
      formData.append('password', this.password.toString())
      fetch('/app/server/register', {
        method: 'POST',
        body: formData
      }).then(response => {
        if (response.ok) {
          router.push({
            path: '/start',
            params: { login: this.login }
          })
        }
      })
    }
  }
}
</script>

<style>
form {
  //display: flex;
  //text-align: center;
}
</style>
