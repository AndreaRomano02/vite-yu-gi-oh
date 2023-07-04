<script>
const endpoint = 'https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons';

import axios from 'axios';
import { store } from '../assets/data/store.js'

export default {
  created() {
    this.getPokemonsType()
  },
  data: () => {
    return {
      options: store.options,
      userSelect: '',
    }
  },
  methods: {
    getPokemonsType() {
      axios.get(`${endpoint}/types1`).then(res => {
        res.data.forEach(option => {
          this.options.push(option);
        })
      })
    },
  },
  emits: ['change-type']
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
