<template>
  <section class="wrapper">
    <div class="hero">
      <h1>IP Adress Tracker</h1>
      <div class="input-div">
        <input class="input" type="text" v-model="ip" placeholder="Search for any IP adress or domain">
        <button class="input-button" v-on:click="getData()">></button>
      </div>
    </div>
    <div class="stats">
      <div class="adress">
        <h2>IP Adress</h2>
        <p v-if="information.length == 0">127.0.0.1</p>
        <p v-else>{{ information.ip }}</p>
      </div>
      <div class="location">
        <h2>Location</h2>
        <p v-if="information.length == 0">Brooklyn, NY 10001</p>
        <p v-else>{{ information.location.city }}, {{ information.location.region }} {{ information.location.postalCode }}</p>
      </div>
      <div class="timezone">
        <h2>Timezone</h2>
        <p v-if="information.length == 0">UTC -05:00</p>
        <p v-else>{{ information.location.timezone }}</p>
      </div>
      <div class="isp">
        <h2>ISP</h2>
        <p v-if="information.length == 0">SpaceX</p>
        <p v-else>{{ information.isp }}</p>
      </div>
    </div>
    <div class="map">
    </div>
  </section>
</template>

<script>
import axios from "axios";

const URL = "https://geo.ipify.org/api/v1?apiKey=at_Y3YT6QNu08weV4NVWA2klUWJ3Twtn&ipAddress="

export default {
  name: 'App',
  data() {
    return {
      ip: "",
      information: [],
    }
  },
  methods: {
    getData() {
      axios.get(URL + this.ip).then(res => {
      this.information = res.data;
      })
    },
  },
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-size: 15px;
  font-family: sans-serif;
}

.hero {
  background-image: url("assets/pattern-bg.png");
  background-repeat: round;
  color: white;
  text-align: center;
  padding: 100px;
}

.wrapper {
  display: flex;
  flex-direction: column;
}

h1 {
    margin-top: 0;
    margin-bottom: 15px;
    font-size: 35px;
}

h2 {
  font-size: 15px;
  opacity: 40%;
  text-transform: uppercase;
  font-weight: 400;
}

p {
  margin-top: 5px;
  font-size: 25px;
}

.input {
  border-radius: 10px;
  box-sizing: border-box;
  border: none;
  width: 400px;
  height: 50px;
  padding-left: 20px;
}

.input-button {
  color: white;
  height: 50px;
  width: 50px;
  margin-left: -20px;
  background-color: black;
  border: none;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}

.stats {
  margin-top: -50px;
  padding: 20px;
  display: flex;
  justify-content: center;
  background-color: white;
  box-shadow: 2px 2px 50px rgba(14, 14, 14, 0.192);
  border-radius: 10px;
  margin-left: auto;
  margin-right: auto;
}

.adress {
  padding: 25px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-right: 1px solid rgb(189, 189, 189);
}

.location {
  padding: 25px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-right: 1px solid rgb(189, 189, 189);
}

.timezone {
  padding: 25px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-right: 1px solid rgb(189, 189, 189);
}

.isp {
  padding: 25px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.map {
  margin-top: -100px;
  background-image: url("assets/map.png");
  background-repeat: no-repeat;
  width:  1886px;
  height: 600px;
  z-index: -5000;
  padding: 8px;
}

</style>