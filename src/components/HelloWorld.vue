<template>
  <v-container>
    <v-card class="ma-2" v-for="(pokemon, id) in pokemons" :key="id">
      <v-list-item three-line>
        <v-list-item-content class="ma-2">
          <v-list-item-title class="text-h5 mb-1">{{
            pokemon["pokemon_name"]
          }}</v-list-item-title>
          <v-list-item-subtitle>{{ pokemon["form"] }}</v-list-item-subtitle>
        </v-list-item-content>

        <v-list-item-avatar tile size="80" color="grey">
          <img
            v-bind:src="
              'https://raw.githubusercontent.com/Purukitto/pokemon-data.json/master/images/pokedex/thumbnails/' +
              getTrueArray(pokemon) +
              '.png'
            "
            alt="pokemon.png"
          />
        </v-list-item-avatar>
      </v-list-item>
       <p class="ma-2 ml-6">Type:</p>
      <v-card-actions>
        <div class="d-flex justify-content-center ma-2">
          <div
            class="ml-2"
            v-for="poki in pokemon['type']"
            :key="poki"
            outlined
            rounded
            text
          >
            {{ poki}}
          </div>
        </div>
      </v-card-actions>
        <p class="ma-2 ml-6">Weakness:</p>
      <v-card-actions>
        <div class="d-flex justify-content-center ma-2">
          <p
            class="ml-2"
            v-for="weakness in getWeaknesses(pokemon)"
            :key="weakness"
            outlined
            rounded
            text
          >
            {{ weakness}}
          </p>
        </div>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data: () => {
    return {
      pokemons: [],
      types: [],
      vulnerabilitys: {
        Bug: {
          Fire: 0.225,
          Flying: 0.225,
          Rock: 0.225,
        },
        Dark: {
          Bug: 0.225,
          Fairy: 0.225,
          Fighting: 0.225,
        },
        Dragon: {
          Dragon: 0.225,
          Fairy: 0.225,
          Ice: 0.225,
        },
        Electric: {
          Ground: 0.225,
        },
        Fairy: {
          Poison: 0.225,
          Steel: 0.225,
        },
        Fighting: {
          Fairy: 0.225,
          Flying: 0.225,
          Psychic: 0.225,
        },
        Fire: {
          Ground: 0.225,
          Rock: 0.225,
          Water: 0.225,
        },
        Flying: {
          Electric: 0.225,
          Ice: 0.225,
          Rock: 0.225,
        },
        Ghost: {
          Dark: 0.225,
          Ghost: 0.225,
        },
        Grass: {
          Bug: 0.225,
          Fire: 0.225,
          Flying: 0.225,
          Ice: 0.225,
          Poison: 0.225,
        },
        Ground: {
          Grass: 0.225,
          Ice: 0.225,
          Water: 0.225,
        },
        Ice: {
          Fighting: 0.225,
          Fire: 0.225,
          Rock: 0.225,
          Steel: 0.225,
        },
        Normal: {
          Fighting: 0.225,
        },
        Poison: {
          Ground: 0.225,
          Psychic: 0.225,
        },
        Psychic: {
          Bug: 0.225,
          Dark: 0.225,
          Ghost: 0.225,
        },
        Rock: {
          Fighting: 0.225,
          Grass: 0.225,
          Ground: 0.225,
          Steel: 0.225,
          Water: 0.225,
        },
        Steel: {
          Fighting: 0.225,
          Fire: 0.225,
          Ground: 0.225,
        },
        Water: {
          Electric: 0.225,
          Grass: 0.225,
        },
      },
      loading: true,
      errored: false,
      opa: 1,
    };
  },
  mounted() {
    this.getPokemons();
    this.getVulnerabilitys();
  },
  methods: {
    getWeaknesses(pokemon) {
      let weaknesses = [];
      pokemon.type.forEach((type) => {
        for (let key in this.vulnerabilitys[type]) {
          if (this.vulnerabilitys[type][key] < 0.3) {
            weaknesses.push(key);
            weaknesses = [...new Set(weaknesses)];
          }
        }
      });
      return weaknesses;
    },
    getTrueArray(pokemon) {
      if (pokemon.pokemon_id <= 9) {
        return "00" + pokemon.pokemon_id;
      }
      if (pokemon.pokemon_id > 9 && pokemon.pokemon_id <= 99) {
        return "0" + pokemon.pokemon_id;
      }
      if (pokemon.pokemon_id > 99) {
        return pokemon.pokemon_id;
      }
    },
    async getPokemons() {
      this.loading = true;
      try {
        const response = await axios.get(
          "https://pokemon-go1.p.rapidapi.com/pokemon_types.json",
          {
            headers: {
              "x-rapidapi-host": "pokemon-go1.p.rapidapi.com",
              "x-rapidapi-key":
                "b663b6236fmsh5b27a567601af4cp110cd7jsnf15d8987a17d",
            },
          }
        );
        this.pokemons = response.data;
        this.loading = false;
      } catch (e) {
        console.error(e);
      }
    },
    async getVulnerabilitys() {
      this.loading = true;
      try {
        const response = await axios.get(
          "https://pokemon-go1.p.rapidapi.com/type_effectiveness.json",
          {
            headers: {
              "x-rapidapi-host": "pokemon-go1.p.rapidapi.com",
              "x-rapidapi-key":
                "b663b6236fmsh5b27a567601af4cp110cd7jsnf15d8987a17d",
            },
          }
        );
        this.types = response.data;
        this.loading = false;
      } catch (e) {
        console.error(e);
      }
    },
  },
};
</script>
