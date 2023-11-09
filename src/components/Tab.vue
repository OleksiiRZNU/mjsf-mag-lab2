<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "Tab",
  props: [ 'target', 'label', 'isActive' ],
  methods: {
    handleClick() {
      this.$emit('activate');
    }
  }
})
</script>

<template>
  <li class="nav-item" role="presentation" @click="handleClick">
    <a class="nav-link" :class="{'active': isActive}" :id="target" data-mdb-toggle="tab" :href="`#${target}`" role="tab"
       :aria-controls="target" aria-selected="false">{{ label }}</a>
  </li>
</template>

<style scoped>

</style>