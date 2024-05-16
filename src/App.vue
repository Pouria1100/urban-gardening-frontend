<template>

  <div>
    <div class="header">
      <h1>U</h1>
      <img src="./assets/logo.png" alt="Urban Garden Logo" />
      <h1>G</h1>
    </div>

    <!--START OF STATUS Panel-->
    <div class="status">
      <h4>Garden Status</h4>
      <!-- First row container -->
      <div class="status-row1">
        <div class="status-row_light">
          <label>Light:</label>
          <span><!-- Light Value --></span>
        </div>
        <div class="status-row_moisture">
          <label>Moisture:</label>
          <span><!-- Moisture Value --></span>
        </div>
      </div>
      <!-- Second row container-->
      <div class="status-row2">
        <div class="status-row_temp">
          <label>Temperature:</label>
          <span><!-- Temperature Value -->°C</span>
        </div>
        <div class="status-row_humidity">
          <label>Humidity:</label>
          <span><!-- Humidity Value -->%RH</span>
        </div>
      </div>
    </div>
    <!--END OF STATUS-->

    <!--START OF GARDENS-->
    <div class="gardens-container">
      <!-- Garden 1 -->
      <div class="garden1">
        <div class="sensor_container">
          <h5>West Garden</h5>
          <div class="sensor_pair">
            <div class="light_sensor1">
              <label>Light:</label>
              <span><!-- Light Sensor 1 Value --></span>
            </div>
            <div>
              <label>Artificial: </label>
              <toggler-button @button-on-click="toggle"  :component="13"></toggler-button>
            </div>
          </div>
          <div class="sensor_pair">
            <div class="humidity_sensor1">
              <label>Humidity:</label>
              <span><!-- Humidity Sensor 1 Value --></span>
            </div>
            <div class="temperature_sensor1">
              <label>Temperature:</label>
              <span><!-- Temperature Sensor 1 Value --></span>
            </div>
          </div>
          <div class="sensor_pair">
            <div class="liquid-value">
              <label>Liquid:</label>
              <span><!-- Liquid Value East Garden --></span>
            </div>
            <div class="moisture_sensor2">
              <label>Moisture:</label>
              <span><!-- Moisture Sensor 2 Value --></span>
            </div>
          </div>
          <div class="sensor_pair">
            <div>
              <label>Pump: </label>
              <toggler-button @button-on-click="toggle"  :component="2"></toggler-button>
            </div>
            <div>
              <label>Fan: </label>
              <toggler-button @button-on-click="toggle"  :component="8"></toggler-button>
            </div>
          </div>
        </div>
      </div>

      <!-- Garden 2 -->
      <div class="garden2">
        <div class="sensor_container">
          <h5>East Garden</h5>
          <div class="sensor_pair">
            <div class="light_sensor2">
              <label>Light:</label>
              <span><!-- Light Sensor 2 Value --></span>
            </div>
            <div>
              <label>Artificial: </label>
              <toggler-button @button-on-click="toggle" :component="12"></toggler-button>
            </div>
          </div>
          <div class="sensor_pair">
            <div class="humidity_sensor2">
              <label>Humidity:</label>
              <span><!-- Humidity Sensor 2 Value --></span>
            </div>
            <div class="temperature_sensor2">
              <label>Temperature:</label>
              <span><!-- Temperature Sensor 2 Value --></span>
            </div>
          </div>
          <div class="sensor_pair">
            <div class="liquid-value">
              <label>Liquid:</label>
              <span><!-- Liquid Value East Garden --></span>
            </div>
            <div class="moisture_sensor2">
              <label>Moisture:</label>
              <span><!-- Moisture Sensor 2 Value --></span>
            </div>
          </div>
          <div class="sensor_pair">
            <div>
              <label>Pump: </label>
              <toggler-button @button-on-click="toggle" :component="4"></toggler-button>
            </div>
            <div>
              <label>Fan: </label>
              <toggler-button @button-on-click="toggle" :component="7"></toggler-button>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>




</template>



<script>

import TogglerButton from './components/TogglerButton.vue'



export default {
  name: 'App',
  components: {
    TogglerButton

  },
  methods: {

    async updateDevicesState(data) {

      const url = 'https://urban-gardening-env-1.eba-vz2yug2s.eu-west-2.elasticbeanstalk.com/component/';

      try {
        const response = await fetch(url, {
          method: 'POST', // Specify the method to use
          headers: {
            'Content-Type': 'application/json' // Specify the content type to be JSON
          },
          body: JSON.stringify(data) // Convert the JavaScript object to a JSON string
        });

        if (!response.ok) {
          throw new Error('Network response was not ok');
        }

        const responseData = await response.json(); // Parse JSON response
        console.log('Device updated successfully:', responseData);
        return responseData; // Return the response data for further processing
      } catch (error) {
        console.error('Error updating device:', error);
        throw error; // Re-throw the error for caller handling
      }


    },

    toggle(data) {

      this.updateDevicesState(data);
    },
  },
}

</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  padding: 0;
  margin: 0;
  background-color: rgb(160, 255, 198);
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 100%;
  height: 100px;
  padding: 0;
  background: rgb(1, 46, 17);
  overflow: hidden;
}



@keyframes moveUpDown {

  0%,
  100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-20px);
  }
}

.header h1 {
  flex: 1;
  text-align: center;
  font-size: 400%;
  cursor: pointer;
  animation: moveUpDown 2s ease-in-out infinite alternate;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}




.header img {
  height: 100px;
  width: auto;
}


.status h4 {
  border-radius: 0 0 15px 15px;
  padding: 5px;
  background-color: rgb(44, 163, 111);
  border-top: 0;
}

.status {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  padding: 0;
}

.status-row1,
.status-row2 {
  display: flex;
  justify-content: space-between;
  width: 100%;
  margin: 5px 0;
}

.status-row_light,
.status-row_moisture,
.status-row_temp,
.status-row_humidity {
  flex: 1;
  background: rgb(52, 187, 128);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
  height: 40px;
}

.status-row_light,
.status-row_temp {
  border-radius: 0 25px 25px 0;
}

.status-row_moisture,
.status-row_humidity {
  border-radius: 25px 0 0 25px;
}

.gardens-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  width: 95%;
  height: 400px;
  overflow-y: auto;
  border-radius: 15px;
  box-sizing: border-box;
  margin: 0 auto;
}


.sensor_container {
  width: 95%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 15px;

}




.sensor_container h5 {
  border-radius: 10px 10px 15px 15px;
  padding: 5px;
  background-color: rgb(44, 163, 111);
  border-top: 0;
  margin: auto 0;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  width: 100%;
}


.sensor_pair {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  border-radius: 25px;
  overflow: hidden;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}



.sensor_pair>div {
  flex: 1;
  width: 95%;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
  background-color: rgb(107, 189, 154);
  padding: 10px;
  margin: 2px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}



.garden1,
.garden2 {
  width: 95%;
  height: 85%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: rgb(233, 255, 219);
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.632), 0 2px 4px rgba(0, 0, 0, 0.627);
  box-sizing: border-box;
  margin: 20px auto;
}





.garden1 .sensor_container>div,
.garden2 .sensor_container>div {
  margin: 5px;
  padding: 10px;
  background-color: rgb(211, 255, 205);
  border: 1px solid rgb(180, 250, 181);
  border-radius: 5px;
  text-align: center;
}

.garden1 button,
.garden2 button {
  padding: 5px 20px;
  font-size: 0.7rem;
  color: white;
  background-color: rgb(34, 133, 79);
  border: none;
  border-Radius: 5px;
  cursor: pointer;
  transition: backgroundColor 0.3s ease;
}

.garden1 button:hover,
.garden2 button:hover {
  background-color: rgb(25, 100, 60);
}
</style>
