<template>
  <div data-app>
    <v-app-bar app color="deep-purple accent-4" dark dense>
      <v-app-bar-nav-icon @click="drawer = true"> </v-app-bar-nav-icon>
      <v-toolbar-title>TitanTicketP</v-toolbar-title>
      <v-spacer></v-spacer>
      <register-modal v-if="!$store.state.isUserLoggedIn" />
      <login-modal v-if="!$store.state.isUserLoggedIn" />
      <v-btn to="logout" v-if="$store.state.isUserLoggedIn">Logout</v-btn>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group v-model="group" active-class="deep-purple--text text--accent-4">
          <v-list-item v-for="item in navItems" :key="item.title" link :to="item.to">
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
import LoginModal from '@/components/Login.vue'
import RegisterModal from '@/components/Registration.vue'

export default {
  data: () => ({
    drawer: false,
    group: null,
    navItems: [
      { title: 'Home', icon: 'mdi-home', to: '/' }
    ]
  }),
  components: {
    LoginModal,
    RegisterModal
  }
}
</script>

<style scoped>

</style>
