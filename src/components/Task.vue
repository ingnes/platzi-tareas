<template lang="pug">

  .container    
    .field.is-horizontal
      .field-label.is-normal
        label.label Titulo
      .field-body
        .field
          p.control
            input.input.is-medium.is-rounded(v-model="title", type="text" placeholder="Titulo")
            span.is-small {{ title }}

    .field.is-horizontal
      .field-label.is-normal
        label.label Tiempo
      .field-body
        .field
          p.control
            input.input.is-medium(v-model="time", type="number" placeholder="Tiempo")
            span.is-small {{ time }}
   
    .field.is-grouped
      p.control
        button.button.is-success.is-medium(@click="addNewTask") Nueva Tarea
      p.control
        button.button.is-danger.is-medium(@click="cancelar") Cancelar
    .field
      .label.label  {{ totalTime }}   
  
    p.is-danger(v-show="!showTasks") {{ 'No hay tareas cargadas' }}
    .table-containter
      table.table.is-bordered.is-striped(v-show="showTasks")
        thead
          th Titulo
          th Tiempo
          th Acciones
            
        tbody
          tr(v-for="(t,i) in tasks",:key="i")
            td {{ t.title }}
            td {{ t.time }}
            td
              button.button.is-danger(@click="removeTask(i)") ❌
</template>

<script>
export default {
  name: 'TaskView',

  data() {
    return {
      tasks: [],
      title: '',
      time: null,
      showTasks: false,
    }
  },

  computed: {
    totalTime() {
      return ` Total de tiempo trabajado ${this.tasks.reduce(
        (a, b) => a + parseInt(b.time),
        0
      )}`
    },
  },

  created() {
    this.cargaTareas()
  },

  methods: {
    addNewTask() {
      if (!this.title || !this.time) {
        return false
      }

      const task = { title: this.title, time: this.time }

      this.tasks.push(task)
      this.showTasks = true
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
      this.title = ''
      this.time = null
    },
    removeTask(indice) {
      this.tasks.splice(indice, 1)
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
      this.tasks.length ? (this.showTasks = true) : (this.showTasks = false)
    },

    cancelar() {
      this.title = ''
      this.time = null
    },
    cargaTareas() {
      this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
      this.tasks.length ? (this.showTasks = true) : (this.showTasks = false)
    },
  },
}
</script>
