
<template>

 
  <div id="app">
    
    <header> 
     
    </header>
    <main>
     
      <img src="./assets/logo.svg" alt="" class="logo"> 
   
      <img src="./assets/180619084-a56960ab-7efa-4e34-9d33-4e3e581d62ff.png" alt="" class="logo"> 
      <input class="input is-large" type="text" placeholder="Pesquise o pokemon" v-model="busca">
      <button class="button is-success is-large is-fullwidth" id="buscarBtn" @click="buscar">buscar</button>
      <div v-for="(poke,index) in filteredPokemons  " :key="poke.url">
        <pokemon id="pokemon" :name="poke.name" :url="poke.url" :num="index + 1"/>
    </div>
    </main>
    
  </div>
</template>
<script>
import axios from 'axios';
import pokemon from './components/pokemon.vue'
export default {
  components:{
    pokemon    
      },
  name:'app',
  data(){
    return{
      pokemons:[],
      filteredPokemons:[],
      busca:''
    }
  },
  created:function(){
    console.log(axios.isCancel('something'));
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0.').then(res =>{
      console.log("pegou a lista de pokemons")
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })

  },computed:{
    // resultadoBusca:function () {
    //   if (this.busca == '' || this.busca  == ' ') {
    //     return this.pokemons
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    //   }
    // }
  },methods:{
    buscar:function () {
      this.filteredPokemons = this.pokemons
      if (this.busca == '' || this.busca  == ' ') {
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
}
</script>
<style scoped>
header {
  line-height: 1.6;
}
#pesquisar{
 margin-top: 5%;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
  padding-bottom: 20%;
  padding-top: 30%;
}
#pokemon{
  padding-top: 5%;
}
@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
