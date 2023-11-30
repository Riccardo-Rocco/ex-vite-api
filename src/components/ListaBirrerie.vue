<script>
import axios from 'axios';

export default {
  data() {
    return {
      birrerie: [],
    };
  },
  mounted() {
    axios.get('https://api.openbrewerydb.org/v1/breweries?by_country=poland&per_page=10')
      .then(response => {
        this.birrerie = response.data;
      })
      
  },
};
</script>


<template>
  <div>
    <h1>Elenco delle Birrerie in Polonia</h1>
    <ul>
      <li v-for="birreria in birrerie" :key="birreria.id">
        {{ birreria.name }}
      </li>
    </ul>
  </div>
</template>



<style>

</style>
