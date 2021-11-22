<template>
  <div class="wrap">
    <div class="search">
      <button type="submit" class="searchSend" v-on:click="getTemperature()">
        <i class="fa fa-search"></i>
      </button>
      <input
        type="text"
        class="searchInput"
        placeholder="Buscar"
        id="input-search"
        v-on:keyup.enter="getTemperature()"
      />
    </div>
    <div class="sizedbox"></div>
    <div class="content">
      <img :src="icon" class='icon-clima'/>
      <h1>{{ city }}</h1>
      <h1>Temperatura: {{ temperature }}ºC</h1>
      <h1>Umidade: {{ humidity }}%</h1>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PrevisaoTempo",
  props: {},
  data() {
    return {
      city: "Cidade",
      temperature: "--",
      humidity: "--",
      icon: null,
    };
  },
  methods: {
    async getTemperature() {
      try {
        var cityAux = document.getElementById("input-search").value;
        const key = "005682ea564601aa6aadafaefe4d92c7";
        var url =
          "https://api.openweathermap.org/data/2.5/weather?q=" +
          cityAux +
          "&appid=" +
          key +
          "&lang=pt_br";
        var response = await axios.get(url);
        this.city = response["data"]["name"];
        this.icon =
          "http://openweathermap.org/img/wn/" +
          response["data"]["weather"][0]["icon"] +
          "@2x.png";
        this.humidity = response["data"]["main"]["humidity"];
        this.temperature = (
          parseFloat(response["data"]["main"]["temp"]) - 273.15
        ).toFixed(1);
        document.getElementById("input-search").value = "";
      } catch (error) {
        console.log("ERRO" + error);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css?family=Poppins&display=swap");
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.search {
  width: 100%;
  height: 50px;
  position: relative;
  display: flex;
  color: #ffffff;
  background-color: #ffffff;
  border-radius: 10px;
}

::placeholder {
  color: #6377ee;
}

.searchInput {
  width: 100%;
  border: 0px solid #6377ee;
  border-radius: 10px;
  outline: none;
  color: #6377ee;
  font-size: 16px;
  font-weight: 700;
}

.searchTerm:focus {
  color: #6377ee;
}

.searchSend {
  width: 40px;
  border: 0px solid #6377ee;
  background: #ffffff;
  text-align: center;
  color: #6377ee;
  border-radius: 10px;
  cursor: pointer;
  font-size: 20px;
}

.wrap {
  width: 80%;
  position: absolute;
  left: 10%;
}

.content {
  color: #ffffff;
}

.icon-clima{
  width: 150px;
}

.sizedbox {
  height: 80px;
}
</style>
