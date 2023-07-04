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
  <h1 class="text-center m-5">POKEDEX</h1>
  <select v-model="store.userSelect">
    <option value="">...</option>
    <option v-for="option in store.options">{{ option }}</option>

  </select>
</template>

<style></style>
