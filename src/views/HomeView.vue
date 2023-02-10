<script setup>
import { onMounted, reactive, ref, computed } from "vue";
import ListPokemons from "../components/ListPokemons.vue"
import SelectedCard from "../components/SelectedCard.vue"

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/")
let pokemons = reactive(ref());
let searchPokemonField = ref("")
let pokemonSelected = reactive(ref());
let loading = ref(false)

onMounted(()=>{
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
  .then(response => response.json())
  .then(response => pokemons.value = response.results);
})

const pokemonsFiltered = computed(()=>{
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon=>
      pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    )
  }
  return pokemons.value;
})

const selectPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(response => response.json())
  .then(response => pokemonSelected.value = response)
  .catch(error => alert(error))
  .finally(()=> loading.value = false)  
}

String.prototype.capitalize = function() {
	return this.charAt(0).toUpperCase() + this.substr(1);
}


</script>

<template>
  <main>
    <div class="container text-body-secondary">
      
      <div class="row mt-4">
        <div class="col-sm-12 col-md-6">
          <SelectedCard
          :name="pokemonSelected?.name.capitalize()"
          :xp="pokemonSelected?.base_experience"
          :height="pokemonSelected?.height"
          :weight="pokemonSelected?.weight"
          :type="pokemonSelected?.types.map(types => types.type.name).toString().capitalize()"
          :img="pokemonSelected?.sprites.other.dream_world.front_default"
          :loading="loading"

          />
      </div>

        <div class="col-sm-12 col-md-6">
          <div class="card card-list">
            <div class="card-body row">
              
              <div class="mb-3">
                <label 
                hidden 
                for="searchPokemonField" 
                class="form-label">
                Pesquisar...
                </label>

                <input 
                v-model="searchPokemonField"
                type="text" 
                class="form-control" 
                id="searchPokemonField" 
                placeholder="Pesquisar...">
              </div>

              <ListPokemons 
              v-for="pokemon in pokemonsFiltered"
              :key="pokemon.name"
              :name="pokemon.name.capitalize()"
              :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
              @click="selectPokemon(pokemon)"
              />
            </div>
          </div>
        </div>

        
      </div>

    </div>
  </main>
</template>

<style scoped>

main {
  background-color: #900e0e;
}

.card-list{
  background-color: #DFDFDF;
  max-height: 75vh;
  overflow-y: scroll;
  overflow-x: hidden;
}

::-webkit-scrollbar{
  background-color: white;
  width: 10px;
}


::-webkit-scrollbar-thumb{
  background: rgb(157, 155, 155);
}



@media (max-width: 768px) {
  .card-list{
    max-height: 48vh;
  }
}
</style>