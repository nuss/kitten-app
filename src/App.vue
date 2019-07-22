<template>
  <div id="app">
    <div>My Kitten App</div>
    <div>
      <div>Kitten of the day:</div>
      <div>
        <div v-if="selectedKitten">{{ selectedKitten.name }}</div>
        <img
            :src="require('./assets/images/' + selectedKitten.img)"
            class="kitten-image">
      </div>
    </div>
    <div>
      <div>Select your favourite kitten:</div>
      <div v-for="kitten in filteredKittens">
        <div>
          {{ kitten.name }}
        </div>
        <img
          :src="require('./assets/images/' + kitten.img)"
          class="kitten-image">
      </div>
    </div>
  </div>
</template>

<script>
import { KITTEN_DATA } from './assets/data';

export default {
  name: 'app',
  data() {
    return {
      kittens: KITTEN_DATA,
      selectedKitten: null,
    };
  },
  computed: {
    // return all kittens except the currently selected
    filteredKittens() {
      return this.kittens
        .filter(kitten => kitten.name !== this.selectedKitten.name);
    }
  },
  created() {
    // set the first kitten as "kitten of the day"
    this.selectedKitten = this.kittens[0];
  }
}
</script>

<style>
html {
  background-color: #F0F0F0;
}

h1 {
  font-size: 36px;
  font-weight: bolder;
  font-family: 'Raleway', Helvetica, Arial, sans-serif;
}

h2 {
  font-size: 24px;
}

h5 {
  font-weight: bolder;
  margin: 0;
}

#app {
  font-family: 'Lato', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  text-align: center;
  color: #2c3e50;
  margin-top:30px;
}

.kitten-image {
  max-height: 100px;
}

.kitten-card {
  background: white;
  border-radius: 4px;
  box-shadow: 0 0 3px 0 rgba(0,0,0,.05);
  text-align: left;
}
</style>
