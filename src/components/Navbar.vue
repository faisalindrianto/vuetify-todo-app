<template>
  <nav>
    <v-toolbar flat app>
      <v-icon right @click.stop="drawer = !drawer">menu</v-icon>
      <v-toolbar-title class="text-uppercase grey--text ml-2">
        <span class="font-weight-light">My</span>
        <span>Todo</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text color="grey">
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" absolute temporary class="primary">
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