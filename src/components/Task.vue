<template lang="pug">

  .container
    .columns.is-centered 
      .column.is-narrow.is-three-fifths   
        .field      
          label.label.has-text-left.is-size-5 Titulo      
          .control
              input.input.is-medium.is-rounded(v-model="title", type="text" placeholder="Titulo")
              //- span.is-small {{ title }}

        .field      
            label.label.has-text-left.is-size-5 Tiempo
            .control
                input.input.is-medium(v-model="time", type="number" placeholder="Tiempo")
                //- span.is-small {{ time }}
    
    .columns.is-centered 
      .column.is-narrow.is-three-fifths 
        .field.is-grouped
          .control
              button.button.is-success.is-medium(@click="addNewTask") Nueva Tarea
          .control
              button.button.is-danger.is-medium(@click="cancelar") Cancelar      
   
    .columns.is-centered 
      .column.is-narrow.is-three-fifths
        p.is-danger.has-text-weight-bold.has-text-left(v-show="!showTasks") {{ 'No hay tareas cargadas' }}
        .table-containter
          table.table.is-bordered.is-striped(v-show="showTasks")
            thead
              th.has-text-centered Titulo
              th.has-text-centered Tiempo
              th.has-text-centered Acciones
                
            tbody
              tr(v-for="(t,i) in tasks",:key="i")
                td {{ t.title }}
                td {{ t.time }}
                td
                  button.button.is-danger(@click="removeTask(i)") ❌
            tfoot
                tr 
                  td.has-text-right.has-text-weight-bold {{ 'Total tiempo de tareas' }}                 
                  td.has-text-weight-bold {{ totalTime }}
                  td
                  
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
      return `${this.tasks.reduce((a, b) => a + parseInt(b.time), 0)}`
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
