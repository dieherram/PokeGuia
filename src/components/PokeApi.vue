<template>
  <div row>
      <h1>PokeGuía</h1>
      <p>Nombre</p>
      <input v-model="pokemonName" @keyup.enter="searchPokemon" type="text">
      <button @click="searchPokemon">Buscar</button>
      <img v-if="currentPokemon.sprites" :src="currentPokemon.sprites.other.dream_world.front_default">
      
      <h3>MOVES</h3>
      <ul>
          <li v-for="move in moves" :key="move.name">
              {{move.move.name}}
          </li>
      </ul> 
      <h3>ABILITIES</h3>
      <ul>
          <li v-for="ability in abilities" :key="ability.name">
              {{ability.ability.name}}
          </li>
      </ul>
  </div>
</template>

<script>
export default {
    data() {
        return {
            currentPokemon: {},
            pokemonName: ""
        }
    },
    created() {
      fetch(`https://pokeapi.co/api/v2/pokemon/pikachu`)
      .then(response => response.json())
      .then(data => this.currentPokemon = data)
    },
    methods: {
        searchPokemon () {
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.lower}`) 
            .then(data => data.json())
            .then(response => this.currentPokemon = response)
        }
    },
    computed:{
        moves() {
return this.currentPokemon.moves
        },
        abilities (){
            return this.currentPokemon.abilities
        },
        lower() {
            return this.pokemonName.toLowerCase()
        }
    }
    
}
</script>

<style>

</style>