<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>
{{info['1']['type']}}
      <v-col class="mb-4">
        <v-card class="mx-auto" max-width="344" outlined>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="text-overline mb-4">OVERLINE</div>
              <v-list-item-title class="text-h5 mb-1">
              
              </v-list-item-title>
              <v-list-item-subtitle
                >Greyhound divisely hello coldly
                fonwderfully</v-list-item-subtitle
              >
            </v-list-item-content>

            <v-list-item-avatar
              tile
              size="80"
              color="grey"
            ></v-list-item-avatar>
          </v-list-item>

          <v-card-actions>
            <v-btn outlined rounded text> Button </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => {
    return {
    pokemons: null,
    loading: true,
    errored: false,
    opa: 1,
    }
  },
  mounted() {
    this.axios
      .get('https://pokemon-go1.p.rapidapi.com/pokemon_types.json',
        {'headers':{'x-rapidapi-host': 'pokemon-go1.p.rapidapi.com',
    'x-rapidapi-key': 'b663b6236fmsh5b27a567601af4cp110cd7jsnf15d8987a17d'}})
      .then(response => (this.info = response.data))
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (console.log(this.info),
        this.loading = false));
  },
}
</script>
