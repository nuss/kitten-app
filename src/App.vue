<template>
  <div id="app">
    <div>
      <h1>My Kitten App</h1>
    </div>
    <!-- <div> -->
      <h2>Kitten of the day:</h2>
      <div class="kitten-card selected-kitten centered">
        <div>
          <h5 v-if="selectedKitten">{{ selectedKitten.name }}</h5>
          <p>
            {{ selectedKitten.age }}<br>
            Fur color: {{ selectedKitten.furColor }}<br>
            Favourite food: {{ selectedKitten.favouriteFood }}
          </p>
        </div>
        <div
          :style="{'background-image': `url(${require('./assets/images/' + selectedKitten.img)})`}"
          class="kitten-image">
        </div>
        <div class="like-buttons">
          <button class="like"></button>
          <button class="dislike"></button>
        </div>
      </div>
    <!-- </div> -->
    <div>
      <h2>Select your favourite kitten:</h2>
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

.selected-kitten {
  display: grid;
  margin-left: auto;
  margin-right: auto;
}

button {
  background-color: white;
  background-position: center;
  background-repeat: no-repeat;
  background-size: contain;
  border-style: none;
  cursor: pointer;
  display: block;
}

button.heart {
  background-image: url(/static/img/heart.svg);
  height: 22px;
  width: 100%;
  margin: 10px auto;
}

button.heart.fav {
  background-image: url(/static/img/heart_full.svg);
}

.like-buttons {
  display: flex;
  margin: 10px auto;
  justify-content: center;
}

button.like,
button.dislike {
  height: 22px;
  width: 40px;
}

button.like {
  background-image: url(/static/img/like.svg);
}

button.dislike {
  background-image: url(/static/img/dislike.svg);
}
</style>
