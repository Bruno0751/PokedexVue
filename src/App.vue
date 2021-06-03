<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <LogoAPI />
      <Api />
      <div class="control">
        <input
          name="txtNomePokemon"
          id="buscarPokemon"
          class="input is-focused"
          type="text"
          placeholder="Buscar Pokemon"
          v-model="buscar"
          style="text-align: center; border-radius: 11px"
        />
      </div>
      <!--
        COENTÁRIO NECESSÁRIO PARA RETORNAR DADOS DA BUSCA, POIS FUNÇÃO JS ESTA COMENTADA
      <div class="buttons">
        <button class="button is-success" @click="buscarPokemons">Success</button>
      </div>
      -->
      <!--
        O :KEY DO V-FOR PRECISA SER UNICO NO CASO É PASSADO COMO CHACVE A URL
      -->
      <div v-for="(pokemon, index) in resultadoBusca" :key="pokemon.url">
        <Pokemon :url="pokemon.url" :name="pokemon.name" :num="index + 1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
import Api from './components/BotaoAPI'
import LogoAPI from './components/LogoAPI'
export default {
  name: "App",
  components: {
    Pokemon,
    Api,
    LogoAPI,
  },
  data() {
    return {
      pokemons: [],
      // NECESSÁRIO PARA PESQUISA QUANDO PRECIONAR O BOTÃO DE BUSCA
      filteredPokemons: [],
      // NECESSÁRIO PARA BUSCA AUTOMÁTICA
      buscar: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        this.pokemons = res.data.results;
        // NECESSÁRIO PARA PESQUISA QUANDO PRECIONAR O BOTÃO DE BUSCA
        this.filteredPokemons = res.data.results;
      });
  },
  // PESQUISAR COM BOTÃO
  /*
  methods: {
    buscarPokemons() {
      this.filteredPokemons = this.pokemons;
      if (this.buscar == "" || this.buscar == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.buscar
        );
      }
    },
  },
  */
  // PESQUISA AUTOMÁTICA
  computed: {
    resultadoBusca: function () {
      if (this.buscar == "" || this.buscar == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter((pokemon) => pokemon.name == this.buscar);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: rgb(108, 213, 245);
  margin: 0;
}
</style>
