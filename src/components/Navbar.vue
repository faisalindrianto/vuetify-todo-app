<template>
  <nav>
    <v-snackbar v-model="snackbar" :timeout="4000" top color="success">
      <span>Awesome! You added a new project.</span>
      <v-btn text color="white" @click="snackbar = false">Close</v-btn>
    </v-snackbar>
    <v-toolbar flat app>
      <v-icon right @click.stop="drawer = !drawer">menu</v-icon>
      <v-toolbar-title class="text-uppercase grey--text ml-2">
        <span class="font-weight-light">My</span>
        <span>Todo</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <v-menu offset-y>
      <template v-slot:activator="{ on }">
        <v-btn outlined v-on="on" color="grey">
          <v-icon left>expand_more</v-icon>
          <span>Menu</span>
        </v-btn>
      </template>
      <v-list>
          <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
            <v-list-item-title>
              {{ link.text }}
            </v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>

      <v-btn text color="grey">
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" absolute temporary class="primary">
      <v-layout column align-center>
        <v-flex class="mt-5">
          <v-avatar size="100">
            <img src="/avatar-1.png" alt="">
          </v-avatar>
          <p class="white--text subtitle-1">Indrianto</p>
        </v-flex>

        <v-flex>
          <Popup @projectAdded="snackbar = true" />
        </v-flex>
      </v-layout>
      <v-list>
        <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
          <v-list-item-action>
            <v-icon class="white--text">{{link.icon}}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-content-title class="white--text">{{link.text}}</v-list-item-content-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
import Popup from './Popup'
  export default {
    components: {
      Popup
    },
    data() {
      return {
        drawer: null,
        links: [
          {icon: 'dashboard', text: 'Dashboard', route:'/'},
          {icon: 'folder', text: 'My Projects', route:'/projects'},
          {icon: 'person', text: 'Team', route:'/teams'},
        ],
        snackbar: false
      }
    },
  }
</script>