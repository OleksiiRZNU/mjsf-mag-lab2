<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "TabContent"
})
</script>

<template>
  <div class="tab-pane fade show active" id="ex1-tabs-3" role="tabpanel" aria-labelledby="ex1-tab-3">
    <slot></slot>
  </div>
</template>

<style scoped>

</style>