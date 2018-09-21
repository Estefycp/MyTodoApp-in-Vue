
<template>
  
  <div >
    <h1 class="card-panel  deep-purple darken-3">My ToDo App</h1>
    <form class="row" @submit.prevent="addTask">
       <button type="submit" class="btn btn-danger col-sm-4 "> Agregar Tarea </button>
      <input class="col-sm-8" v-model="newTaskName" type="text">
     
    </form>

   <div class="row">
      <tasks-list
          class="col s7 push-s5"
          :title="'Pendientes'"
          :task-list="tasksPending"
          :icon="'label_outline'"
          @completar="toggleTasks"/>
      

        <tasks-list
          class="col s7 pull-s5"
          :title="'Completados'"
          :task-list="tasksComplete"
          :icon="'done'"
          @completar="toggleTasks"/>

      </div>
  </div>
</template>

<script>
import TasksList from './components/TasksList'

const storageKey = 'storage';

export default {
  components: {
    TasksList
  },
  data () {
    return {
      newTaskName: '',
      tasks: [
        {
          name: 'Tarea 1',
          done: false
        },
        {
          name: 'Tarea 2',
          done: false
        },
        {
          name: 'Tarea 2',
          done: false
        }
      ]


      
    }
  },
  created(){
    this.tasks = JSON.parse(localStorage.getItem(storageKey));
  },
  methods: {
    toggleTasks (task) {
      task.done = !task.done
    },
    addTask () {
      if (!this.newTaskName) return
      this.tasks.push({ name: this.newTaskName, done: false })
      this.newTaskName = ''

      
    }
  },
  computed: {
    tasksPending () {
      localStorage.setItem(storageKey,JSON.stringify(this.tasks));
      return this.tasks.filter(task => !task.done)
    },
    tasksComplete () {
      localStorage.setItem(storageKey,JSON.stringify(this.tasks));
      return this.tasks.filter(task => task.done)
    }
  }



 
}
</script>