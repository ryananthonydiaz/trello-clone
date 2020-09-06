<template>
  <div class="task-view">
    <div
      class="flex flex-col flex-grow items-start justify-between px-4"
    >
      {{ taskName }}
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getTask']),
    task () {
      return this.getTask(this.$route.params.id)
    },
    taskName () {
      if (this.task) {
        return this.task.name
      }
      return ''
    }
  }
}
</script>

<style>
.task-view {
  @apply relative flex flex-row bg-white pin mx-4 m-32 mx-auto py-4 text-left rounded shadow;
  max-width: 700px;
}
</style>
