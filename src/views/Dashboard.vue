<template>
  <div class="dashboard">

    <v-container class="my-5">
    <h1 class="grey--text mb-4">Dashboard</h1>
      <v-layout row class="mb-3 ml-1">
        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn small depressed class="mr-2" @click="sortBy('title')" v-on="on">
              <v-icon left>folder</v-icon>
              <span class="caption text-lowercase">By project name</span>
            </v-btn>
          </template>
          <span>sort by project name</span>
        </v-tooltip>

        <v-tooltip top>
          <template v-slot:activator="{ on }">
            <v-btn small depressed @click="sortBy('person')" v-on="on">
              <v-icon left>person</v-icon>
              <span class="caption text-lowercase">By person</span>
            </v-btn>
          </template>
          <span>sort by person name</span>
        </v-tooltip>
      </v-layout>

      <v-card outlined class="pa-3 pl-5" v-for="project in projects" :key="project.title">
        <v-layout row :class="`pa-3 project ${project.status}`">
          <v-flex xs12 md6>
            <div class="caption grey--text">Project Title</div>
            <div>{{ project.title }}</div>
          </v-flex>
          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">Person</div>
            <div>{{ project.person }}</div>
          </v-flex>
          <v-flex xs6 sm4 md2>
            <div class="caption grey--text">Due By</div>
            <div>{{ project.due }}</div>
          </v-flex>
          <v-flex xs2 sm4 md2>
            <div>
              <v-chip right small :class="`${project.status} white--text`">{{ project.status }}</v-chip>
            </div>
          </v-flex>
        </v-layout>
      </v-card>
    </v-container>
  </div>
</template>

<script>
import db from '@/fb'
export default {
  data(){
    return{
      projects: []
    }
  },
  mounted(){

  },
  methods: {
    sortBy(prop){
      this.projects.sort((a, b) => a[prop] < b[prop] ? -1 : 1)
    }
  },
  created(){
    db.collection('projects').onSnapshot(res => {
      const changes = res.docChanges()

      changes.forEach(change => {
        if(change.type === 'added'){
          this.projects.push({
            ...change.doc.data(),
            id: change.doc.id
          })
        }
      })
    })
  }
}
</script>

<style>
.project.complete{
  border-left: 4px solid #3CD1C2;
}
.project.ongoing{
  border-left: 4px solid orange;
}
.project.overdue{
  border-left: 4px solid tomato;
}
.v-chip.complete{
  background: #3CD1C2 !important;
}
.v-chip.ongoing{
  background: orange !important;
}
.v-chip.overdue{
  background: tomato !important;
}
</style>