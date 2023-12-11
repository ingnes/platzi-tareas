<template lang="pug">
  tsk-header
  tsk-task 
</template>

<script>
import TskHeader from '@/components/TaskHeader.vue'
import TskTask from '@/components/Task.vue'

export default {
  name: 'App',

  components: { TskHeader, TskTask },
}
</script>

<style lang="scss">
@import '@/scss/main.scss';
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
