<template>
  <v-app id="app" light toolbar>
    <v-navigation-drawer :mini-variant.sync="mini" v-model="drawer" light enable-resize-watcher persistent overflow>
      <v-toolbar flat class="transparent">
        <v-list class="pa-0">
          <v-list-tile avatar>
            <v-list-tile-avatar>
              <img src="https://randomuser.me/api/portraits/men/85.jpg" />
            </v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title>John Leider</v-list-tile-title>
            </v-list-tile-content>
            <v-list-tile-action>
              <v-btn icon @click.native.stop="mini = !mini">
                <v-icon>chevron_left</v-icon>
              </v-btn>
            </v-list-tile-action>
          </v-list-tile>
        </v-list>
      </v-toolbar>
      <v-list class="pa-0" dense>
        <v-divider></v-divider>
        <v-list-tile v-for="item in menuItems" :key="item.title" :to="item.link">
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile
          v-if="userIsAuthenticated"
          @click="onLogout">
          <v-list-tile-action>
            <v-icon>exit_to_app</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>Logout</v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar class="primary" fixed dark>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="white--text">
        <router-link to="/" tag="span" style="cursor: pointer">Tab Tracker</router-link>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items class="hidden-xs-only">
        <v-btn flat v-for="item in menuItems" :key="item.title" :to="item.link">
          <v-icon left dark>{{ item.icon }}</v-icon>
          {{ item.title }}
        </v-btn>
        <v-btn
          v-if="userIsAuthenticated"
          flat
          @click="onLogout">
          <v-icon left dark>exit_to_app</v-icon>
          Logout
        </v-btn>
      </v-toolbar-items>
    </v-toolbar>
    <main fixed>
      <v-container fluid>
        <router-view></router-view>
      </v-container>
    </main>
    <v-footer fixed class="primary">
      <span class="white--text"> © 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        drawer: true,
        mini: false,
        right: null
      }
    },
    computed: {
      menuItems() {
        let items = [{
              icon: 'face',
              title: 'Sign Up',
              link: '/signup'
            },
            {
              icon: 'lock_open',
              title: 'Sign In',
              link: '/signin'
            }
          ]
        return items
      }
    },
    methods: {}
  }
</script>
