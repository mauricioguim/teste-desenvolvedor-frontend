<template>
  <main class="form-signin">
    <form @submit.stop.prevent="submit">
      <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

      <div class="form-floating">
        <input type="email" class="form-control" id="floatingInput" placeholder="name@example.com" v-model="email">
        <label for="floatingInput">Email address</label>
      </div>
      <div class="form-floating">
        <input type="password" class="form-control" id="floatingPassword" placeholder="Password" v-model="password">
        <label for="floatingPassword">Password</label>
      </div>
      <button class="w-100 bFtn btn-lg btn-primary" type="submit">Sign in</button>
    </form>
  </main>
</template>

<script>
import Cookie from 'js-cookie';

export default {
  name: "Login-app",
  data () {
    return {
      email: '',
      password: ''
    }
  },

  methods: {
    submit () {
      const payload = {
        email: this.email,
        password: this.password
      }
      fetch('http://localhost:8000/api/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'Accept': 'application/json',
          'X-Requested-With': 'XMLHttpRequest'
        },
        body: JSON.stringify(payload)
      })
      .then(response => response.json())
      .then(res =>
          Cookie.set('app_token', res.access_token, { expires: 1 }))
      .then(function () {
        window.location.href = '/';
      })
    }
  }

}
</script>

<style scoped>
.form-signin {
  width: 100%;
  max-width: 330px;
  padding: 15px;
  margin: auto;
}

.form-signin .checkbox {
  font-weight: 400;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
