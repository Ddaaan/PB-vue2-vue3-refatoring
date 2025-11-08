<template>
  <div class="container">
    <!-- v-for -->
    <ul>
      <li v-for="item in items" :key="item.id">
        {{ item.name }}
      </li>
    </ul>

    <!-- v-if / v-show / style binding -->
    <div>
      <div v-if="isVisible">This is visible 1</div>
      <div :style="{ visibility: isVisible ? 'visible' : 'hidden' }">
        This is visible 2
      </div>
      <div v-show="isVisible">This is visible 3</div>
      <button @click="toggleVisible">Toggle Visibility</button>
    </div>

    <!-- v-text / v-html / v-pre / 조건 분기 -->
    <div>
      <div v-text="count"></div>
      <div v-html="countHtml"></div>
      <div v-pre>{{ count }}</div>

      <div v-if="count % 3 === 0">count % 3 === 0</div>
      <div v-else-if="count % 2 === 0">count % 2 === 0</div>
      <div v-else>Count is not divisible by 2 or 3</div>

      <button @click="increment">Increment Count</button>
    </div>
  </div>

  <!--
   directives
   1. v-if
   2. v-else
   3. v-else-if
   4. v-show
   5. v-for
   6. v-on
   7. v-bind
   8. v-model
   9. v-slot
   10. v-text
   11. v-html
   12. v-pre
   13. v-cloak
   14. v-once
   15. v-is
   16. v-memo
  -->
</template>

<script setup>
import { ref, computed } from 'vue'

const isVisible = ref(true)
const items = ref([
  { id: 1, name: 'Item 1' },
  { id: 2, name: 'Item 2' },
  { id: 3, name: 'Item 3' },
  { id: 4, name: 'Item 4' }
])

const count = ref(0)
const countHtml = computed(() => `<strong>${count.value}</strong>`)

const toggleVisible = () => {
  isVisible.value = !isVisible.value
}

const increment = () => {
  count.value++
}
</script>

<style scoped>
.container {
  display: grid;
  width: 300px;
  margin: 0 auto;
  padding: 20px;
  grid-gap: 20px;
}
</style>
