<template>
  <div id="app">
    <h1 class="title">VueJS Crypto App</h1>
    <div class="card" v-for="(rate, index) in rates" :key="index">
      <p>
        {{ index }}:
        <span class="float-right">{{ rate }} {{ currency }}</span>
      </p>
    </div>
    <div class="text-center">
      <button id="reload" title="Reload page" @click="reloadApp">
        <i class="fas fa-redo"></i>
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data: function() {
    return {
      rates: [],
      coins: ["BTC", "ETH", "XRP", "LTC", "EOS", "XMR"],
      currency: "RON" //You can change here the currency
    };
  },
  methods: {
    reloadApp: function() {
      location.reload();
    }
  },
  mounted: function() {
    axios
      .get(
        `http://api.coinlayer.com/api/live?access_key=b1238dece839e7dd3e5379f1d13a733d&target=${this.currency}&symbols=${this.coins}`
      )
      // `http://api.coinlayer.com/api/live?access_key=b1238dece839e7dd3e5379f1d13a733d&target=${this.currency}&symbols=BTC,ETH,XRP,LTC,EOS,XMR`
      .then(promise => (this.rates = promise.data.rates))
      .catch(error => console.error(error))
      .finally(console.log("API Loaded."));
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.12.0-2/css/all.min.css");

* {
  margin: 0;
  padding: 0;
  outline: 0;
  box-sizing: border-box;
}
*:focus {
  outline: 0;
}
body {
  color: #f0f0f0;
  background-color: #191919;
  font-family: "Montserrat", sans-serif;
}
#app {
  margin-top: 20px;
  width: 100%;
}
.card {
  padding: 20px 15px;
  background-color: #333333;
  width: 50%;
  margin: 0 auto;
  margin-bottom: 15px;
  transition: all 0.3s ease-in-out;
}
#reload {
  font-size: 30px;
  padding: 12px 14px;
  border: none;
  border-radius: 50%;
  color: #f0f0f0;
  background-color: #333333;
  transition: all 0.3s ease-in-out;
  cursor: pointer;
  box-shadow: 2px 4px 4px 2px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
}
#reload:hover {
  background-color: #404040;
}
#reload:active {
  background-color: #505050;
}
.card:hover {
  background-color: #454545;
}
.container {
  width: 80%;
  margin: 0 auto;
}
.float-right {
  float: right;
}
.title {
  margin: 20px 0px;
  text-align: center;
  font-weight: 400;
}
.text-center {
  width: 100%;
  text-align: center;
  margin: 0 auto;
}
</style>
