<template>
  <div class="home">
    <h1>Home</h1>
    <input type="text" v-model="search">
    <p>Search term - {{ search }}</p>
    <div v-for="name in matchingNames" :key="name">
      {{ name }}
    </div>
    <button @click="handleClick">Stop watching</button>
  </div>
</template>

<script>
import { ref, computed } from '@vue/reactivity'
import { watch, watchEffect } from '@vue/runtime-core'


export default {
  name: 'HomeView',
  setup() {
    const search = ref('')
    const names = ref(['mario', 'yoshi', 'luigi', 'wilson', 'jeffrey', 'buena', 'pogi'])

    const stopWatch = watch(search, () => {
      console.log('watch function ran');
    })

    const stopEffect = watchEffect(() => {
      console.log('watch effect function ran', search.value)
    })
    const matchingNames = computed(() => {
      return names.value.filter(name => name.includes(search.value))
    })

    const handleClick = () => {
      stopWatch()
      stopEffect()
    }
    return { names, search, matchingNames, handleClick }
  },
}
</script>
