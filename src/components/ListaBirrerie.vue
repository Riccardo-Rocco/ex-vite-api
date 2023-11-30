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
        <h2>{{ birreria.name }}</h2>
        <p>Posizione: {{ birreria.country }}</p>
        <p>Coordinate: {{ birreria.latitude }}, {{ birreria.longitude }}</p>
        <p>Indirizzo: {{ birreria.adress1 }}, {{ birreria.city }}, {{ birreria.state_province }}, {{ birreria.postal_code }}</p>
        <hr>
      </li>
    </ul>
  </div>
</template>



<style>

</style>
