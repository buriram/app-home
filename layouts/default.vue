<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" app right>
      <v-toolbar flat>
        <v-list>
          <v-list-tile>
            <v-list-tile-title class="title">Main Menu</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-toolbar>
      <v-divider/>
      <v-list dense class="pt-0">
        <v-list-tile v-for="item in items" :key="item.title">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title><nuxt-link :to="item.url">{{ item.title }}</nuxt-link></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>

    <v-toolbar app class="cyan darken-2" dark>
      <v-toolbar-title style="cursor: pointer" @click="homeClick"><v-icon class="green lighten-3">home</v-icon> RooMBooKing Wellcome </v-toolbar-title>
      <v-spacer/>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"/>
    </v-toolbar>
    <v-content>
      <nuxt/>
    </v-content>
    <v-footer class="pa-3" color="grey lighten-1">
      <v-spacer>Power By VEC (All right reserved)</v-spacer>
      <div>&copy; {{ new Date().getFullYear() }}</div>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: 'Home', icon: 'home', url: '/' },
        { title: 'Room', icon: 'update', url: '/room' },
        { title: 'Booking', icon: 'assignment_turned_in', url: '/booking' },
        { title: 'Chat', icon: 'group', url: '/chat' },
        { title: 'key', icon: 'security', url: '/keyroom' },
        { title: 'Logout', icon: 'lock', url: '/Logout' },
      ],
      right: null,
    }
  },
  computed: {
    online: {
      get() {
        return this.$store.state.online
      },
      set(value) {
        this.$store.commit('setOnline', value)
      },
    },
    drawer: {
      get() {
        return this.$store.state.drawer
      },
      set(value) {
        this.$store.commit('setDrawer', value)
      },
    },
  },

  mounted() {
    this.$store.commit('setOnline', window.navigator.onLine)
    window.addEventListener('offline', this.toggleNetworkStatus)
    window.addEventListener('online', this.toggleNetworkStatus)
  },

  beforeDestroyed() {
    window.removeEventListener('offline', this.toggleNetworkStatus)
    window.removeEventListener('online', this.toggleNetworkStatus)
  },

  methods: {
    toggleNetworkStatus({ type }) {
      this.online = type === 'online'
    },
    homeClick() {
      this.$router.replace('/')
    },
  },
}
</script>
