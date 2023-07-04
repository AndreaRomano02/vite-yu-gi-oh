<script>
import { store } from '../assets/data/store.js'

export default {
  data: () => {
    return {
      options: store.options,
      userSelect: '',
    }
  },
}
</script>

<template>
  <select v-model="userSelect" @change="$emit('change-type', userSelect)">
    <option value="">...</option>
    <option v-for="option in options">{{ option }}</option>
  </select>
</template>

<style scoped>
select {
  margin-left: 30px;
}
</style>
