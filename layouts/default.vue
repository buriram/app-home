<template>
  <v-app class="light-blue darken-3" dark>
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

    <v-toolbar app class="light-blue darken-4" dark>
      <v-toolbar-title style="cursor: pointer" @click="homeClick"><v-icon class="green lighten-3">home</v-icon> Wellcome</v-toolbar-title>
      <v-spacer/>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"/>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt/>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: 'Home', icon: 'home', url: '/student-list' },
        { title: 'memo', icon: 'group', url: '/Record' },
        { title: 'Recordings', icon: 'group', url: '/recordings' },
        { title: 'Chat', icon: 'group', url: '/chat' },
        { title: 'Logout', icon: 'group', url: '/' },
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
