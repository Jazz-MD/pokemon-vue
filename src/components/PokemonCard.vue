<script>
export default {
  name: 'PokemonCard',
  props: {
    pokemonName: {
      type: String
    },
    imageUrl: {
      type: String
    }
  },
  data() {
    return {
      userInput: '',
      correct: false
    }
  },
  methods: {
    sendName() {
      console.log(this.pokemonName)
      if (this.userInput.toLowerCase().trim() == this.pokemonName.toLowerCase()) {
        this.correct = true
        this.$emit('send-name', this.pokemonName)
      } else {
        alert('Siga participando')
      }
    }
  }
}
</script>
<template>
  <div class="card card-title text-center col-3 align-items-center">
    <img :class="!correct ? 'filter' : ''" :src="imageUrl" :alt="pokemonName" />
    <div v-if="correct">
      <p class="name">{{ pokemonName }}</p>
    </div>
    <form v-else @submit.prevent="sendName">
      <input v-model="userInput" />
      <button>Descubrir</button>
      <p class="incorrect" v-show="correct == false">Incorrecto, Intenta Nuevamente</p>
    </form>
  </div>
</template>
<style scoped>
.filter {
  filter: blur(5px) grayscale(100%);
}
</style>
