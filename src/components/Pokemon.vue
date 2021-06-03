<template>
  <div class="pokemon">
    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentIMG "
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>
        <div class="content">
          <button class="button is-fullwidth is-primary is-light" @click="mudarSprite()">Mudar Posição</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  // CRIAR CONEXEO
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.pokemon.type = res.data.types[0].type.name;
      this.currentIMG = this.pokemon.front;
    });
  },
  // CRIA VARIAVEIS ,aRRAYS E OBJETOS
  data() {
    return {
      isFront: true,
      currentIMG: '',
      pokemon: {
        front: '',
        type: '',
        back: ''
        },
    };
  },
  // DEFINE PROPS PARA RECEBER ELEMENTOS DE OUTROS COMPONENTES
  props: {
    num: Number,
    url: String,
    name: String,
  },
  // ADICIONA FILTROS GERALMENTE AOS TEXTOS
  filters: {
    upper: function (value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
  // CRIAR FUNÇOES
  methods: {
    mudarSprite(){
      if(this.isFront){
        this.isFront = false
        this.currentIMG = this.pokemon.back
      }else{
        this.isFront = true
        this.currentIMG = this.pokemon.front
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pokemon{
  margin-top: 11px;
}
</style>
