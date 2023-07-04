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
      userText: '',
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
  emits: ['change-type', 'search-text', 'reset-text']
}
</script>

<template>
  <div class="d-flex">

    <select class="form-select w-25" v-model="userSelect" @change="$emit('change-type', userSelect)">
      <option value="">...</option>
      <option v-for="option in options">{{ option }}</option>
    </select>

    <input v-model="userText" @keyup="$emit('search-text', userText)" type="text" placeholder="Cerca..."
      class="form-control ms-5 w-25">
    <span class="ms-2" title="Delete filter">
      <font-awesome-icon @click="$emit('reset-text', userText = '')" icon="fa-solid fa-xmark" size="2xl"
        style="color:red; cursor:pointer;" />
    </span>
  </div>
</template>

<style scoped>
select {
  margin-left: 30px;
}
</style>
