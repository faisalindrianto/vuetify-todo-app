<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on }">
        <v-btn color="white" v-on="on">Add New Project</v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">Add New Project</span>
        </v-card-title>
        <v-card-text>
          <v-form class="px-3 py-2" ref="form">
            <v-text-field label="title" v-model="title" prepend-icon="folder" :rules="inputRules"></v-text-field>
            <v-textarea label="information" v-model="content" prepend-icon="edit" :rules="inputRules"></v-textarea>
            <v-menu
              v-model="menu2"
              :close-on-content-click="false"
              :nudge-right="40"
              transition="scale-transition"
              offset-y
              min-width="290px"
            >
              <template v-slot:activator="{ on }">
                <v-text-field
                  v-model="due"
                  label="Due Date"
                  prepend-icon="event"
                  readonly
                  v-on="on"
                ></v-text-field>
              </template>
              <v-date-picker v-model="due" @input="menu2 = false"></v-date-picker>
            </v-menu>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">Close</v-btn>
          <v-btn color="primary" text @click="submit" class="mr-3" :loading="loading">Add Project</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  import db from '@/fb'
  export default {
    data(){
      return{
        dialog: false,
        title: '',
        content: '',
        date: new Date().toISOString().substr(0, 10),
        menu2: false,
        inputRules: [
          v => v.length >= 3 || 'Minimal 3 karakter slur'
        ],
        loading: false
      }
    },
    methods: {
      submit(){
       if(this.$refs.form.validate()){
         this.loading = true
         const project = {
           title: this.title,
           content: this.content,
           due: this.due,
           person: 'Faisal',
           status: 'ongoing'
         }

         db.collection('projects').add(project).then(() => {
           this.loading = false
           this.dialog = false
           this.$emit('projectAdded')
         })
       }
      }
    }
  }
</script>