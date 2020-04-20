<template>
  <nav>
    <v-toolbar flat app>
      <v-btn color="pink" dark @click.stop="drawer = !drawer">
        Toggle
      </v-btn>
      <v-toolbar-title class="text-uppercase grey--text ml-2">
        <span class="font-weight-light">My</span>
        <span>Todo</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text color="grey">
        <span>Sign Out</span>
        <v-icon right>mdi-exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <p>test</p>
    </v-navigation-drawer>
  </nav>
</template>

<script>
  export default {
    data() {
      return {
        drawer: null,
        items: [{
            title: 'Home'
          },
          {
            title: 'About'
          },
        ],
      }
    },
  }
</script>