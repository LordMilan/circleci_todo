<template>
  <div class="home">
  
     <v-text-field
            v-model="newTaskTitle"
            @click:append="addTask"
            @keyup.enter="addTask"
            class="pa-5"
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            hide-details
            clearable
          >
      </v-text-field>

      <v-alert
      :value="alert"
      class="ma-5"
      dense
      outlined
      type="error"
    >
      Please Enter <strong>Task</strong> to <strong>Add.</strong>
    </v-alert>

    <v-list
      flat >
      <v-subheader>Tasks: </v-subheader>
<div v-for="task in tasks" :key="task.id">
          <v-list-item 
          @click="doneTask(task.id)"
          :class="{ 'blue lighten-5' : task.done}"
          >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
              class="text-capitalize"
              :class="{ 'text-decoration-line-through' : task.done }"
              >
                {{ task.title}}
                </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn 
              @click.stop="deleteTask(task.id)"
              icon>
                <v-icon color="red lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
        </div>
      </v-list>
  </div>
</template>

<script>

  export default {
    name: 'Home',
    data() {
      return{
        newTaskTitle: '',
        alert: false,
        tasks: [
          {
            id: 1,
            title: 'Wake up',
            done: false
          },
          {
            id: 2,
            title: 'Eat breakfast',
            done: false
          },
          {
            id: 3,
            title: 'Start work',
            done: false
          }
        ]
      }
    },
    methods:{
      addTask() {
        
          if(this.newTaskTitle.length === 0){
            this.alert= true
          }else{
            let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.alert= false
        this.newTaskTitle = ''
          }
        
        
      },
      doneTask(id){
        console.log(id)
        let task = this.tasks.filter(task => task.id === id)[0]
        task.done = !task.done
        },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id)
      }
    }

    
  }
</script>
