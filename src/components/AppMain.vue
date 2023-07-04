<script>
const endpoint = 'https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons';

import AppFilter from './AppFilter.vue';
// Import lybrary Axios
import axios from 'axios';

// LOGIC
export default {
  components: { AppFilter },
  props: {
    pokemons: Array,
  },
  created() {

    // Riempio l'array dei pokemons al montare della pagina
    this.getPokemons(endpoint);
    this.isLoading = true;
  },
  data() {
    return {
      isLoading: false,
    }
  },
  methods: {
    getPokemons(endpoint) {
      axios.get(endpoint)
        .then(res => {
          res.data.docs.forEach(doc => {
            this.pokemons.push(doc);
          })
        })
        .catch(err => {
          console.error(err.message)
        })
        .then(() => {
          this.isLoading = false
        });
    },
    filterType(userSelect) {
      console.log(userSelect)
    },
  },
  computed: {
    orderedPokemons() {
      return this.pokemons.sort((prev, next) => prev.number > next.number ? 1 : -1)
    },
  }
}
</script>

<template>
  <AppFilter @change-type="this.filterType" />

  <h1 v-if="isLoading" class="loading">LOADING...</h1>
  <div v-else class="container py-5">
    <div class="row row-cols-3 g-4">
      <div v-for="pokemon in orderedPokemons" :key="pokemon.number" class="col">
        <div class="card">
          <div class="card-img-top">
            <img class="img-fluid" :src="pokemon.imageUrl" alt="">
          </div>
          <div class="card-body">
            <p>Number: {{ pokemon.number }}</p>
            <p>Name: <strong>{{ pokemon.name }}</strong></p>
            <p>Type: {{ pokemon.type1 }} <span v-if="pokemon.type2">{{ pokemon.type2 }}</span></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.loading {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-img-top {
  height: 300px;
  border-bottom: 1px solid lightgray;
  padding: 0 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

img {
  max-height: 100%;
}

p {
  align-self: flex-end;
}
</style>
