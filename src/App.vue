<template>
  <v-app>
    <v-main>
      <div class="container">
        <div class="search_container">
          <p class="search_title">Enter a pokemon</p>
          <input v-model="searchData" placeholder="Search" type="text" class="search_input">
        </div>
      </div>
      <HelloWorld :searchData="searchData"/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  data: () => ({
    searchData:"",
  }),
  components: {
    HelloWorld,
  },
};
</script>
