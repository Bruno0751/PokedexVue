<template>
  <div>
    <h1>{{ num }} {{ name | upper}}</h1>
    <small>{{ url }}</small>
  </div>
</template>

<script>
export default {
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
