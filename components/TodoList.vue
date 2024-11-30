<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" md="8">
        <h1 class="text-center">Vuetify To-Do List</h1>

        <!-- Add Task Input -->
        <v-row>
          <v-col cols="9">
            <v-text-field
              v-model="newTask"
              label="Enter a new task"
              outlined
              dense
              @keyup.enter="addTask"
            ></v-text-field>
          </v-col>
          <v-col cols="3">
            <v-btn
              color="primary"
              block
              :disabled="!newTask.trim()"
              @click="addTask"
            >
              Add
            </v-btn>
          </v-col>
        </v-row>

        <!-- Task List -->
        <v-list>
          <v-list-item
            v-for="(task, index) in tasks"
            :key="index"
            :class="{ 'text-decoration-line-through': task.completed }"
          >
            <v-list-item-content>
              <v-list-item-title @click="toggleTask(index)">
                {{ task.text }}
              </v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon color="red" @click="removeTask(index)">
                <v-icon>mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
        </v-list>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      newTask: '', // Holds the input value for a new task
      tasks: [], // List of tasks
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, completed: false })
        this.newTask = '' // Clear input field
      }
    },
    toggleTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed
    },
    removeTask(index) {
      this.tasks.splice(index, 1) // Remove task from the list
    },
  },
}
</script>

<style scoped>
.text-decoration-line-through {
  text-decoration: line-through;
  color: #9e9e9e;
  cursor: pointer;
}
</style>
