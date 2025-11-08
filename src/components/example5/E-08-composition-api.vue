<!-- src/components/example5/E-08-composition-api.vue -->
<template>
  <div>
    <h2>{{ componentTitle }}</h2>
    <p>Full Name: {{ fullName }}</p>
    <input v-model="firstName" placeholder="First Name" />
    <input v-model="lastName" placeholder="Last Name" />
    <button @click="greet">Greet</button>
    <p>Greeting Count: {{ greetCount }}</p>
    <p>{{ message }}</p>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  ref,
  computed,
  watch,
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted
} from 'vue'

export default defineComponent({
  name: 'E08CompositionApi',
  props: {
    title: {
      type: String,
      default: 'User Information'
    }
  },
  setup(props, { expose }) {
    const firstName = ref('John')
    const lastName = ref('Doe')
    const greetCount = ref(0)
    const message = ref('')

    const componentTitle = computed(() => props.title)
    const fullName = computed(() => `${firstName.value} ${lastName.value}`)

    const greet = () => {
      greetCount.value++
      message.value = `Hello, ${fullName.value}!`
    }

    const resetGreetCount = () => {
      greetCount.value = 0
    }

    watch(greetCount, (newValue, oldValue) => {
      console.log(`Greet count changed from ${oldValue} to ${newValue}`)
      if (newValue >= 3) {
        message.value = "That's enough greetings for now!"
      }
    })

    onBeforeMount(() => console.log('beforeMount hook'))
    onMounted(() => console.log('mounted hook'))
    onBeforeUpdate(() => console.log('beforeUpdate hook'))
    onUpdated(() => console.log('updated hook'))
    onBeforeUnmount(() => console.log('beforeUnmount hook'))
    onUnmounted(() => console.log('unmounted hook'))

    // 외부에서 사용할 수 있도록 노출 (원래 defineExpose 역할)
    expose({
      resetGreetCount
    })

    return {
      componentTitle,
      firstName,
      lastName,
      greetCount,
      message,
      fullName,
      greet,
      resetGreetCount
    }
  }
})
</script>
