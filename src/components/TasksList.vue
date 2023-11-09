<script>
import {defineComponent} from 'vue'
import Task from "./Task.vue";

export default defineComponent({
  name: "TasksList",
  components: {Task},
  props: ['tasks'],
  methods: {
    updateStatus(id, status) {
      this.$emit('update-status', id, status);
    }
  }
})
</script>

<template>
  <ul class="list-group mb-0">
    <Task v-for="task in tasks" :key="task.id" :task="task" @update-status="updateStatus"></Task>
  </ul>
</template>

<style scoped>

</style>