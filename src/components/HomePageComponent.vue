<template>
  <div class="homePageComponent">

    <div class="weatherBox">
      <br/>
      <p>{{ locationData.name }},</p><p>{{ locationData.country }}</p>
      <p>{{ locationData.localtime }}</p>

      <img :src="currentData.condition?.icon"/>
      <p>{{currentData.temp_c}}°C {{currentData.temp_f}}°F</p>
      <p>{{ currentData.condition?.text }}</p>
    </div>
    
    <div class="time" >
    <p>Hourly Forecast</p>
      <div class="hour" v-for="(item,i) in hourData" :key="i">
        <h5>{{item.time.slice(10)}}</h5>
        <img :src="item.condition?.icon" />
        <h5>{{item.temp_c}}°C</h5>
        <p>{{ item.condition?.text }}</p>
      </div>
    </div>
    <br />
    <br />
    
  </div>
</template>

<script>

export default {
  name: "HomePageComponent",
  props:{
    currentData:{
        typeof: [],
        require: true
    },
    locationData:{
        typeof: [],
        require: true
    },
    hourData:{
        typeof: [],
        require: true
    }
  },

};
</script>
