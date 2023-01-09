<template>
  <div data-app>
    <v-app-bar app color="gray accent-4" dark dense>
      <v-app-bar-nav-icon @click="drawer = true"> </v-app-bar-nav-icon>
      <v-toolbar-title>TitanTicketP</v-toolbar-title>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary bottom>
      <v-list nav dense>
        <v-list-item-group v-model="group" active-class="deep-purple--text text--accent-4">
          <div v-for="(item, index) in navItems" :key="item.title">
            <div v-if="item.items" :prepend-icon="item.action" no-action>
              <br v-if="index !== 0">
              <v-list-item-title v-text="item.title" no-action text style="text-align:left;"></v-list-item-title>

              <div v-for="subItem in item.items" :key="subItem.title">
                <v-list-item :to="subItem.to" :key="subItem.title" v-if="subItem.stateCheck ? ($store.state[subItem.stateCheck] == subItem.stateStatus) : true">
                    <v-list-item-icon>
                      <v-icon v-text="subItem.action"></v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                      <v-list-item-title v-text="subItem.title"></v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
              </div>
            </div>

            <v-list-item v-else :to="item.to" link>
              <v-list-item-icon>
                <v-icon v-text="item.action"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title v-text="item.title"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </div>
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
      {
        action: '',
        title: 'General',
        items: [
          { title: 'Home', action: 'mdi-home', to: '/' }
        ]
      },
      {
        action: '',
        title: 'Account',
        items: [
          { title: 'Login', action: 'mdi-login', to: '/login', stateCheck: `isUserLoggedIn`, stateStatus: false },
          { title: 'Register', action: 'mdi-account-plus', to: '/register', stateCheck: `isUserLoggedIn`, stateStatus: false },
          { title: 'Logout', action: 'mdi-logout', to: '/logout', stateCheck: `isUserLoggedIn`, stateStatus: true }
        ]
      }
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
