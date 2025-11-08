<!-- src/components/example3/ChildComponent.vue -->
<template>
  <div>
    <p>{{ message }}</p>
    <button @click="$emit('custom-event', 'Hello from child')">Send Event</button>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ChildComponent',
  props: {
    message: {
      type: String,
      required: true
    }
  },
  emits: ['custom-event']
})
</script>
