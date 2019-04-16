<template>
  <section id="app">
    <Card v-for="item in items" :item="item" :key="`item_${item.id}`" />
  </section>
</template>

<script>
const axios = require('axios');

import Card from './components/Card.vue';

export default {
  name: 'app',

  data: function() {
    return {
      items: [],
    }
  },

  components: {
    Card
  },

  created: function () {
    // Get the JSON data
    axios.get('http://prototype.carter-dev.net/fed-test/items.json')
         .then(response => {
           this.items = response.data.items;
         })
         .catch(console.error);
  },
}
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    font-family: "Open Sans", sans-serif;
  }

  #app {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 1em;
    display: grid;
    grid-gap: 1em;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    grid-template-rows: repeat(auto-fit, minmax(400px, 1fr));
  }
</style>