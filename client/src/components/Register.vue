<template>
  <v-layout>
    <v-flex xs6 offset-xs3>
      <div class="white elevation-2">
        <v-toolbar flat dense class="teal lighten-3" dark>
          <v-toolbar-title>Register</v-toolbar-title>
        </v-toolbar>

          <div class="pl-4 pr-4 pt-2 pb-2">
            <form
              name="signup-form"
              autocomolete="off">
              <v-text-field
                label="Email"
                v-model="email"
              ></v-text-field>
              <v-text-field
                label="Username"
                v-model="username"
              ></v-text-field>
              <v-text-field
                label="First Name"
                v-model="firstName"
              ></v-text-field>
              <v-text-field
                label="Last Name"
                v-model="lastName"
              ></v-text-field>
              <v-text-field
                label="Password"
                type="password"
                v-model="password"
              ></v-text-field>
            </form>
            <br>
            <span v-html="error" class="red--text" />
            <br>
            <v-btn
              @click="register"
              class="teal lighten-3">
              Register
            </v-btn>
          </div>

      </div>
    </v-flex>
  </v-layout>
</template>

<script>
import AuthService from '@/services/AuthService'
export default {
  name: 'Register',
  data () {
    return {
      email: '',
      username: '',
      firstName: '',
      lastName: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthService.registerUser({
          email: this.email,
          username: this.username,
          firstName: this.firstName,
          lastName: this.lastName,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        console.log('register button was clicked', response.data)
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
