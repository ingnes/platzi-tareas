<template lang="pug">

section.section
      nav.nav.has-shadow
        .container
          .field
            label.label {{ name }}   
    
</template>

<script>
export default {
  name: 'TaskHeader',

  data() {
    return {
      name: 'Task Manager',
    }
  },
}
</script>
