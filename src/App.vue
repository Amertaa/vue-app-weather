<template>
 <div id="app">
 <main>
   <div class="title">Weather App</div>
   <div class="search-box">
    <input 
    type="text" 
    class="search-bar" 
    placeholder="Search..."
    v-model="query"
    @keypress="fetchWeather"
    />
    
   </div>
   <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
    <div class="location-box">
      <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
      <div class="date">{{dateBuilder()}} </div>

    </div>

      <div class="weather-box">
      <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
      <div class="weather">{{weather.weather[0].main}} </div>
      </div>

   </div>
  </main>
 </div>
</template>

<script>
export default {
  name:'app',
  data(){
    return {
      api_key: '682d9e4a4fe76ca618a8e64b7721e637',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather: {}
    }
  },
  methods: {
     fetchWeather (e) {
       if (e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res. json();
        }).then(this.setResults);
       }
     },
     setResults(results){
       this.weather = results;
     },
     dateBuilder () {
       const d = new Date();
       const months = ["Januari","Februari","Maret","April","May","June","July","August","September", "October","November","December"];
       const days = ["Minggu","Senin","Selasa","Rabu","Kamis","Jumat","Sabtu"];

       const day= days[d.getDay()];
       const date= d.getDate();
       const month= months[d.getMonth()];
       const year= d.getFullYear();
       
       return `${day} ${date} ${month} ${year}`;
     }
  }
}  
</script>

<style>
*{
  margin : 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: 'monsterrat', sans-serif ;
  overflow: hidden;
}
#app{
  background-image: url(../src/assets/weather.jpg); 
  background-size:  cover ;
  background-position: center;
  transition: 0.4s;

}



.title{
color: white;
font-size: 32px;
font-weight: 500;
text-align: center;
text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
padding-bottom: 10px;
}

main {
min-height: 100vh;
padding: 25px;

}


.search-box {
  width: 100%;
  margin-bottom: 30px;

}

.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  border-radius: 15px 0px 15px 0px;
  color: #313131;
  font-size: 20px;

appearance: none;
border: none;
outline: none;
background: none;

box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
background-color:rgba(255, 255, 255, 0.5);
transition: 0.4s;

}

.search-box .search-bar:focus{
box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
background-color: rgba(255, 255, 255, 0.5);
border-radius: 16px 0px 16px 0px;
}

.location-box .location {
color: white;
font-size: 32px;
font-weight: 500;
text-align: center;
text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
color: white;
font-size: 20px;
font-weight: 300;
font-style: italic;
text-align: center

}

.weather-box {
  text-align: center;
}

.weather-box .temp {
display: inline-block;
padding: 10px 25px;
color: white;
font-size: 102px;
font-weight: 900;

text-shadow: 3px 6px rgba(0, 0, 0, 0,25);
background-color:rgba(255, 255, 255, 0.25);
border-radius: 16px;
margin: 30px 0px;

box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather{
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
