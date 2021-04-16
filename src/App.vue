<template>
  <div id="app">
    <img class="logo" src="./assets/pokemon.png" alt="pokemon">

    <div>
      <label for="pokemon">Nombre:</label>
      <input class="mx-2" id="pokemon" v-model="nombre_pokemon" type="text" @keyup.enter="reqPokemon" placeholder="Ingresa un pokemon"/>
      <button class="btn btn-info text-light" @click="reqPokemon">Buscar</button>
    </div>

    <img :src="getImagen" alt="pokemon">


    <div>
      <h2>Moves</h2>
      <ul>
        <li v-for="(move, i) in getMoves" :key="i">
          {{move.move.name}}
        </li>
      </ul>
    </div>

    <div>
      <h2>Abilities</h2>
      <ul>
        <li v-for="(ability, i) in getAbilities" :key="i">
          {{ability.ability.name}}
        </li>
      </ul>
    </div>

<!--     <p>Ability: {{ability}}</p>
    <p>Move: {{move}}</p> -->
  </div>
</template>

<script>

export default {
  name: 'App',
  
  data() {
    return {
      nombre_pokemon: "pikachu",
      arr_Moves: "",
      arr_Abilities: "",
      imagen: ""
    }
  },

    computed: {
      getMoves() {
        return this.arr_Moves
      },
      getAbilities(){
        return this.arr_Abilities
      },
      getImagen(){
        return this.imagen
      }
    },

  methods: {
    async reqPokemon(){
            const url = "https://pokeapi.co/api/v2/pokemon/"

            try {
                const req = await fetch(url + this.nombre_pokemon)
                const data = await req.json()
                console.log(data)
                this.arr_Abilities = data.abilities/* [0].ability.name */
                this.arr_Moves = data.moves/* [0].move.name */
                this.imagen = data.sprites.front_default
            } catch (error) {
                console.log(error)
            }
        },
  },

  created () {
    this.reqPokemon();
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

ul{
  list-style: none;
}
</style>