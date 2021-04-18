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
        <div class="col-md-4">
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

            <div class="card-body text-center">
              <span class="badge badge-pill badge-light" style="font-size: 30px;">{{data.types[0].type.name}}</span>
              <span v-if="data.types[1]" class="badge badge-pill badge-light" style="font-size: 30px;">{{data.types[1].type.name}}</span>
              <table class="table">
                <thead class="thead-dark">
                  <tr>
                    <th scope="col">HP</th>
                    <th scope="col">ATK</th>
                    <th scope="col">DEF</th>
                    <th scope="col">ATK.SP</th>
                    <th scope="col">DEF.PS</th>
                    <th scope="col">AGI</th>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <th scope="row">{{data.stats[0].base_stat}}</th>
                    <th scope="row">{{data.stats[1].base_stat}}</th>
                    <th scope="row">{{data.stats[2].base_stat}}</th>
                    <th scope="row">{{data.stats[3].base_stat}}</th>
                    <th scope="row">{{data.stats[4].base_stat}}</th>
                    <th scope="row">{{data.stats[5].base_stat}}</th>
                  </tr>
                </tbody>
              </table>
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
