<template>
  <div class="pokemons">
    <input type="text" placeholder="Search a pokemon" v-model="search">

    <!-- <v-container>
      <v-card>
        <v-layout v-for="pokemon in filter" :key="pokemon.id" justify-center align-center>
          <v-flex xs6>
            <p id="pokemonName"></p>
            <img src='' id="pokemonImg" />
          </v-flex>

          <v-flex xs6>
            <p @click="fiche(pokemon)">{{ pokemon.name }}</p>
          </v-flex>
        </v-layout>
      </v-card>
    </v-container>-->
    <!-- <v-container grid-list-sm>
      <v-layout row wrap v-for="pokemon in filter" :key="pokemon.id">
        <v-flex d-flex>
          <v-layout row wrap>
            <v-flex d-flex column>
              <p id="pokemonName"></p>
                 <img src='' id="pokemonImg" />
            </v-flex>
          </v-layout>
        </v-flex>
        <v-flex d-flex child-flex>
           <p @click="fiche(pokemon)">{{ pokemon.name }}</p>
        </v-flex>
      </v-layout>
    </v-container>-->
    <!-- <v-container grid-list-sm>
      <v-layout v-for="pokemon in filter" :key="pokemon.id">
        <v-layout>
          <v-flex>
            <p id="pokemonName"></p>
            <img src id="pokemonImg">
          </v-flex>
        </v-layout>
        <v-layout>
          <v-flex>
            <p @click="fiche(pokemon)">{{ pokemon.name }}</p>
          </v-flex>
        </v-layout>
      </v-layout>
    </v-container>-->
    <!-- <div class="container">
      <div class="row" v-for="pokemon in filter" :key="pokemon.id">
        <div class="col-6">
          <p id="pokemonName"></p>
          <img src id="pokemonImg">
        </div>
        <div class="col-6">
          <p @click="fiche(pokemon)">{{ pokemon.name }}</p>
        </div>
      </div>
    </div>-->
    <div class="container">
      <div class="row d-flex justify-center align-center">

        <div class="col-8 height">
          <p id="pokemonName"></p>
          <img src id="pokemonImg">
        </div>

      <div class="col-4">
        <div v-for="pokemon in filter" :key="pokemon.id">
          <p @click="fiche(pokemon)">{{ pokemon.name }}</p>
        </div>
      </div>
      </div>
    </div>


  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      pokemons: [],
      search: ""
    };
  },
  created() {
    axios
      .get(
        "https://raw.githubusercontent.com/Biuni/PokemonGO-Pokedex/master/pokedex.json"
      )
      .then(response => {
        this.pokemons = response.data.pokemon;
        /* eslint-disable no-alert, no-console */
        // console.log(this.pokemons);
      })
      .catch(e => {
        /* eslint-disable no-alert, no-console */
        console.log(e);
      });
  },
  computed: {
    filter() {
      return this.pokemons.filter(
        pokemon =>
          pokemon.num.includes(this.search) ||
          pokemon.name.toLowerCase().includes(this.search.toLowerCase())
      );
    }
  },
  methods: {
    fiche(n) {
      document.getElementById("pokemonName").innerHTML = n.name;
      document.getElementById("pokemonImg").src = n.img;
    }
  }
};
</script>
<style>
.height {
    height: 100px;
}
</style>
