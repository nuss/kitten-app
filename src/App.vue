<template>
  <div id="app">
    <div>
      <h1>My Kitten App</h1>
    </div>
    <div>
      <div>Kitten of the day:</div>
      <div class="kitten-card centered">
        <div v-if="selectedKitten">{{ selectedKitten.name }}</div>
        <div
          :style="{'background-image': `url(${require('./assets/images/' + selectedKitten.img)})`}"
          class="kitten-image">
        </div>
      </div>
    </div>
    <div>
      <div>Select your favourite kitten:</div>
      <div class="kitten-cards">
        <div class="kitten-card" v-for="kitten in filteredKittens" v-bind:key="kitten">
          <div>
           <h5>{{ kitten.name }}</h5>
           <p>
            {{ kitten.age }}<br>
            Fur color: {{ kitten.furColor }}<br>
            Favourite food: {{ kitten.favouriteFood }}
           </p>
          </div>
          <div
            :style="{'background-image': `url(${require('./assets/images/' + kitten.img)})`}"
            class="kitten-image">
          </div>
          <button class="heart" v-bind:class="{ fav: kitten.isFavourite }"></button>
        </div>
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
  background-color: #fff;
  padding: 6px 8px;
  display: inline-block;
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
  font-size: 14px;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

.kitten-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 1000px;
  margin: 0 auto;
  align-content: space-around;
}

.kitten-image {
  height: 100px;
  width: 100%;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.kitten-card {
  text-align: left;
  margin: 5px;
  width: 190px;
}

.kitten-card h5 {
  margin: 10px 10px 0;
}

.kitten-card p {
  margin-left: 10px;
  margin-right: 10px;
}

.kitten-card,
h1 {
  background-color: white;
  border-radius: 4px;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  box-shadow: 0 0 3px 0 rgba(0,0,0,.05);
  -moz-box-shadow: 0 0 3px 0 rgba(0,0,0,.05);
  -webkit-box-shadow: 0 0 3px 0 rgba(0,0,0,.05);
}

.centered {
  margin: 0 auto;
}

button.heart {
  margin: 6px auto;
  border-style: none;
  display: block;
  height: 40px;
  width: 40px;
}
</style>
