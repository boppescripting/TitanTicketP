<!-- <template>
  <v-app>
    <v-layout column>
      <v-container xs6 offset-xs3>
        <div class="white elevation-2">
          <v-toolbar flat dense class="cyan" dark>
            <v-toolbar-title>Register</v-toolbar-title>
          </v-toolbar>

          <div class="pl-4 pr-4 pt-2 pb-2">
            <form autocomplete="off" name="registration-form">
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field label="Email Address" type="email" name="email" v-model="email" autocomplete="email"></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="6">
                    <v-text-field label="Password" type="password" name="password" v-model="password"
                      autocomplete="new-password"></v-text-field>
                  </v-col>
                  <div class="error" v-html="error" />
                  <br>
                  <v-btn block @click="register">Register</v-btn>
                </v-row>
              </v-container>
            </form>
          </div>
        </div>
      </v-container>
    </v-layout>
  </v-app>
</template> -->

<template>
  <v-dialog v-model="dialog" persistent max-width="600px">
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" dark v-bind="attrs" v-on="on">
        Register
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="text-h5">Registration</span>
      </v-card-title>
      <v-card-text>
        <form autocomplete="off" name="registration-form">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field label="* Email Address" type="email" name="email" v-model="email"
                  autocomplete="email"></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="* Password" type="password" name="password" v-model="password"
                  autocomplete="new-password"></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </form>
        <small>
          <div class="error" v-html="error" />
        </small>
        <small>*indicates required field</small>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="blue darken-1" text @click="dialog = false">
          Close
        </v-btn>
        <v-btn color="blue darken-1" text @click="register">
          Create Account
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
      email: '',
      password: '',
      error: null,
      dialog: false
    }
  },
  methods: {
    async register () {
      try {
        this.error = null
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
        this.$emit('close')
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  }
}
</script>

<style scoped>
.error {
  color: red;
}
</style>
