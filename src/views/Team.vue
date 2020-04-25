<template>
  <div class="team">
    <h1 class="subtitle-1 grey--text">Teams</h1>
    
    <v-container class="my-5">
      <v-layout row wrap>
        <v-flex xs12 sm6 md4 lg3 v-for="person in team" :key="person.name">
          <v-card outlined class="text-xs-center ma-2">
            <v-avatar size="100">
              <img :src="person.avatar" alt="" class="mx-auto">
            </v-avatar>
            <v-card-text>
              <div class="title">{{person.name}}</div>
              <div>{{person.role}}</div>
            </v-card-text>
            <v-card-action>
              <v-btn text block color="grey" class="ma-1">
                <v-icon small left>message</v-icon>
                <span>Message</span>
              </v-btn>
            </v-card-action>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
export default {
  data(){
    return {
      team: [
        { name: 'The Net Ninja', role: 'Web developer', avatar: '/avatar-1.png' },
        { name: 'Ryu', role: 'Graphic designer', avatar: '/avatar-2.png' },
        { name: 'Chun Li', role: 'Web developer', avatar: '/avatar-3.png' },
        { name: 'Gouken', role: 'Social media maverick', avatar: '/avatar-4.png' },
        { name: 'Yoshi', role: 'Sales guru', avatar: '/avatar-5.png'}
      ]
    }
  }
}
</script>
