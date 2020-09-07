<template>
  <AppDrop @drop="moveTaskOrColumn">
    <AppDrag
      class="task"
      :transferData="{
        type: 'task',
        fromColumnIndex: columnIndex,
        fromTaskIndex: taskIndex
      }"
      @click="goToTask(task)"
    >
      <span class="w-full flex-no-shrink font-bold">
        {{ taskName }}
      </span>
      <p v-if="descriptionIsPresent" class="w-full flex-no-shrink mt-1 text-small">
        {{ taskDescription }}
      </p>
    </AppDrag>
  </AppDrop>
</template>

<script>
import tasksAndColumns from '@/mixins/tasksAndColumns'
import AppDrop from '@/components/AppDrop'
import AppDrag from '@/components/AppDrag'

export default {
  components: { AppDrop, AppDrag },
  mixins: [tasksAndColumns],
  props: {
    task: {
      type: [Object]
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  computed: {
    taskName () {
      if (this.task === null) {
        return ''
      } else {
        return this.task.name
      }
    },
    taskDescription () {
      if (this.task === null) {
        return ''
      } else {
        return this.task.description
      }
    },
    descriptionIsPresent () {
      return this.taskDescription.length > 0
    }
  },
  methods: {
    goToTask (task) {
      this.$router.push({ name: 'task', params: { id: task.id } })
    }
  }
}
</script>

<style lang="css" scoped>
.task {
  @apply flex items-center flex-wrap shadow mb-2 py-2 px-2 rounded bg-white text-grey-darkest no-underline;
}

.task:hover {
  cursor: move;
}
</style>
