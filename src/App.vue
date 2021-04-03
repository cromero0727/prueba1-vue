<template>
  <div id="app">
    <label class="label">Ingresar Pokemones</label>
    <br>
    <!-- v-model (permite comunicarse con las variables de estado) -->
    <input class="label_input" v-model="pokemon" type="text" />

    <button class="label_button" @click="ingresarPokemon">Ingresar Pokemon</button>

     <ol>
      <!-- Key debe ser un dato primitivo -->
      <li v-for="(pokemon, index) in pokemones" :key="index">
        {{ pokemon }}
      </li>
    </ol>
    
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      pokemones: [],
      pokemon: "",
      
    };
  },
  methods: {
    async getData() {
      const url = "https://pokeapi.co/api/v2/pokemon/";
      try {
        const req = await fetch(url);
        const reqJson = await req.json();
        console.log(reqJson);
      } catch (error) {
        console.log(error);
      }
    },
    ingresarPokemon() {
      if (this.pokemon === "") return;
      this.pokemones.push(this.pokemon);
      this.pokemon = "";
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: justify;
  color: #2c3e50;
  margin-top: 60px;
  
}

.label{
  font-size: 2rem;
  &_input{
    height: 1.5rem;
    border-radius: 4px;
    border: 1px solid #2c3e50;
    margin-right: 5px;
  }
  &_button{
    padding: .5rem 1rem;
    color: #2c3e50;
    background-color: #94caff;
    border: none;
    border-radius: 4px
  }
}
</style>
