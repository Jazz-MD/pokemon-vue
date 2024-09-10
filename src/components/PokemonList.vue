<script>
import axios from 'axios'
import PokemonCard from '@/components/PokemonCard.vue'
export default {
  name: 'PokemonList',
  components: { PokemonCard },
  data() {
    return {
      pokemonList: []
    }
  },
  async mounted() {
    try {
      for (let i = 1; i <= 20; i++) {
        const url = 'https://pokeapi.co/api/v2/pokemon/' + i
        const { data } = await axios.get(url)
        this.pokemonList.push(data)
      }
    } catch (error) {
      console.error('No pudimos atrapar ningún pokemon 😞:', error)
    }
  },
  computed: {
    counter() {
      return this.pokemonList.filter((pokemon) => pokemon.esCorrecto).length
    }
  },
  methods: {
    discovered(pokemonName) {
      const foundPokemon = this.pokemonList.find(
        (pokemon) => pokemon.name.toLowerCase() == pokemonName
      )
      foundPokemon.esCorrecto = true
    }
  }
}
</script>
<template>
  <div class="container">
    <div class="mt-3 d-flex flex-column align-items-center">
      <h1>Quien es ese pokemon</h1>
      <p>Pokemones encontrados {{ counter }}</p>
    </div>
    <div class="row mt-3">
      <PokemonCard
        v-for="(pokemon, idx) in pokemonList"
        :key="idx"
        :pokemonName="pokemon.name"
        :imageUrl="pokemon.sprites.front_default"
        @send-same="discovered"
      />
    </div>
  </div>
</template>
<style scoped></style>
