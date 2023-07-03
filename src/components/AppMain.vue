<script>
import { store } from '../assets/data/store.js'
import axios from 'axios';
export default {

  created() {
    this.getPokemons();
  },
  data() {
    return {
      store,
    }
  }, methods: {
    getPokemons() {
      axios.get('https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons?eq[type1]=Electric&sort[number]=desc').then(
        (res) => {
          res.data.docs.forEach(doc => {
            this.store.pokemons.push(doc)
          });
        }
      )
    },
  },
}
</script>

<template>
  <p v-for="pokemon in store.pokemons">{{ pokemon.name }}</p>
</template>

<style></style>
