<script>
import { store } from '../assets/data/store.js'

export default {
  data: () => {
    return {
      store,
    }
  },
}
</script>

<template>
  <select v-model="store.userSelect" @change="$emit('change-type')">
    <option value="">...</option>
    <option v-for="option in store.options">{{ option }}</option>
  </select>
</template>

<style scoped>
select {
  margin-left: 30px;
}
</style>
