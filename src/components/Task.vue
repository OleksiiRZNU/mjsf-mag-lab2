<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "Task",
  props: ['task'],
  methods: {
    toggleStatus() {
      this.$emit('update-status', this.task.id, this.status)
    }
  },
  data() {
    return {
      status: this.task.completed
    }
  }
})
</script>

<template>
  <li class="list-group-item d-flex align-items-center border-0 mb-2 rounded completed">
    <input class="form-check-input me-2" type="checkbox" value="" aria-label="..." :checked="task.completed" v-model="status" @change="toggleStatus" />
    <template v-if="task.completed"><s>{{ task.text }}</s></template>
    <template v-else>{{ task.text }}</template>
  </li>
</template>

<style scoped>
.completed {
  background-color: #f4f6f7;
}
</style>