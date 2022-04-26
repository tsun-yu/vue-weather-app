<script setup>
import { ref } from "@vue/reactivity";

let api_key = "625d92b4d8d1889d9ae4efc7172270aa";
let base_url = "https://api.openweathermap.org/data/2.5/";
const query = ref("");
const results = ref([]);
const isOnly = (arr) => {
  return arr.length === 1;
};
const isFirst = (i, arr) => {
  return arr.length != 1 && i === 0;
};
const isLast = (i, arr) => {
  return i != 0 && i === arr.length - 1;
};

const getData = async () => {
  try {
    const response = await fetch(
      `${base_url}weather?q=${query.value}&units=metric&APPID=${api_key}`
    );
    const data = await response.json();
    // console.log(data);
    if (data.cod === "404") return;
    const obj = {
      main: data.main,
      name: data.name,
      weather: data.weather,
    };
    console.log(obj);
    results.value.unshift(obj);
    // console.log(results);
  } catch (err) {
    console.log("eee");
  }
};

// getData();
</script>

<template>
  <div class="container">
    <div class="searchWrap">
      <input
        type="text"
        name=""
        id="citySearch"
        placeholder="Search City"
        class="searchBar"
        @keyup.enter="getData"
        v-model="query"
      />
    </div>
    <div class="weatherWrap">
      <div
        class="weatherCard"
        v-for="(v, i) of results"
        :class="{
          'weatherCard--first': isFirst(i, results),
          'weatherCard--last': isLast(i, results),
          'weatherCard--only': isOnly(results),
        }"
        :key="i"
      >
        <h2>{{ v.name }}</h2>
        <p>date</p>
        <h1>{{ v.main.temp }}°C</h1>
      </div>
    </div>
  </div>
</template>

<style>
:root {
  --color-primary: #def4fe;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background-image: url("./assets/4961757.jpg");
  background-size: cover;
  background-position: 50% 0%;
}
#app.cool {
  background-image: url("./assets/6241816.jpg");
}
.container {
  min-height: 100vh;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.searchWrap {
  width: 100%;
  margin-bottom: 2rem;
}
.searchBar {
  display: block;
  width: 100%;
  height: 4rem;
  padding: 1rem 1.5rem;
  font-size: 1.5rem;
  border: none;
  outline: none;
  border-radius: 2rem;
  background-color: rgba(255, 255, 255, 0.3);
  backdrop-filter: blur(10px);
  transition: 0.4s ease-in;
}
.searchBar:focus {
  background-color: rgba(255, 255, 255, 0.7);
  box-shadow: 0 5px 10px rgb(0 0 0 / 12%);
}
.weatherWrap {
  width: 80%;
  max-width: 1000px;
}
.weatherCard {
  width: 100%;
  border-radius: 0.25rem;
  background-color: #def4fee8;
  color: #036684;
  padding: 1rem;
  backdrop-filter: blur(3px);
  transition: 0.4s ease-in;
  margin-bottom: 0.1rem;
}
.weatherCard--first {
  border-radius: 2rem 2rem 0.25rem 0.25rem;
}
.weatherCard--last {
  border-radius: 0.25rem 0.25rem 2rem 2rem;
}
.weatherCard--only {
  border-radius: 2rem 2rem 2rem 2rem;
}
.weatherCard:hover {
  background-color: #70bbde;
  color: #fff;
}
</style>
