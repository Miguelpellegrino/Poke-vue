<template>
  <div class="hello">
    <div class="container-fluid">
      <div class="row justify-content-center">
        <div class="col-md-6">
          <div class="input-group mb-4">
            <input v-model="pokemon" type="text" class="form-control" placeholder="Recipient's username" aria-label="Recipient's username" aria-describedby="basic-addon2">
            <div class="input-group-append">
              <button class="btn btn-outline-secondary" @click="pokemones" type="button">Button</button>
            </div>
          </div>
        </div>
      </div>
     
      <div v-if="data.name" class="row justify-content-center">
        <div class="col-md-4 ">
          <h1 class="text-center text-uppercase">{{data.name}}</h1>
          <div class="card" >
            <img v-if="data.sprites.other.dream_world.front_default" :src="data.sprites.other.dream_world.front_default"
              class="card-img-top" 
              alt="Card image cap" 
              style="width: 100%;">
            <img v-else :src="data.sprites.front_default"
              class="card-img-top" 
              alt="Card image cap" 
              style="width: 100%;">

            <div class="card-body">
              <p><span class="badge badge-light">{{data.types[0].type.name}}</span></p>
              <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
              <a href="#" class="btn btn-primary">Go somewhere</a>
            </div>
          </div>

        </div>
      </div>

      <div v-else class="alert alert-danger" role="alert">
        Debe ingregar un numero o nombre de pokemon
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Pokeapi',
  data(){
    return{
      data:[],
      pokemon:''
    }
  },
  methods: {
    pokemones: function(){
      this.data = axios.get('https://pokeapi.co/api/v2/pokemon/' + this.pokemon).then(response=>{
      this.data = response.data
      console.log(this.data)
      })
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
