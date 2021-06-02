<template>
  <div>
    <h1>{{ num }} {{ name | upper}}</h1>
    <small>{{ url }}</small>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    created: function(){
      axios.get(this.url).then(res => {
         this.pokemon.front = res.data.sprites.front_default
        this.pokemon.back = res.data.sprites.back_default

        this.pokemon.type = res.data.types[0].type.name
        console.log(this.pokemon)
      })
    },
    data(){
      return{
        pokemon: {}
      }
    },
  props: {
    num: Number,
    url: String,
    name: String
  },
  filters: {
    upper: function(value){
      let newName = value[0].toUpperCase() + value.slice(1)
      return newName
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
