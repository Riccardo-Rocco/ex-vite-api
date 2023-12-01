<script>
import axios from 'axios';

export default {
  data() {
    return {
      birrerie: [],
      searchTerm: '', 
    };
  },
  mounted() {
    this.fetchBirrerie();
  },
  methods: {
    fetchBirrerie() {
      axios.get('https://api.openbrewerydb.org/v1/breweries?by_country=poland&per_page=10')
        .then(response => {
          this.birrerie = response.data;
        })
        
    },
   
    search() {
    
      if (this.searchTerm.trim() !== '') {
        
        this.birrerie = this.birrerie.filter(birreria =>
          Object.values(birreria).some(value =>
            String(value).toLowerCase().includes(this.searchTerm.toLowerCase())
          )
        );
      } else {
        
        this.fetchBirrerie();
      }
    },
  },
};
</script>

<template>
  <div>
    <h1>Elenco delle Birrerie in Polonia</h1>
    
    
    <input v-model="searchTerm" @input="search" placeholder="Inserisci il termine di ricerca">
   
    <button @click="search">Cerca</button>
    
    <ul>
      <li v-for="birreria in birrerie" :key="birreria.id">
        <h2>{{ birreria.name }}</h2>
        <p>Posizione: {{ birreria.country }}</p>
        <p>Coordinate: {{ birreria.latitude }}, {{ birreria.longitude }}</p>
        <p>Indirizzo: {{ birreria.address_1 }}, {{ birreria.city }}, {{ birreria.state_province }}, {{ birreria.postal_code }}</p>
        <hr>
      </li>
    </ul>
  </div>
</template>

<style>

</style>
