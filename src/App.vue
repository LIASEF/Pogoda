<template>
  <!-- 05:40 - Основные теги -->
  <div id="app">
    <!-- 16:34 - Условия -->
    <div v-if="errorMessage">{{ errorMessage }}</div>
    <div v-else>
      <!-- 00:35 - Подключение стилей -->
      <h1>Weather App</h1>
      <!-- 02:30 - Описание дизайна -->
      <input type="text" v-model="city" placeholder="Enter city" />
      <button @click="fetchWeather">Get Weather</button>

      <!-- 33:12 - Красивый вывод -->
      <div v-if="weather">
        <h2>{{ weather.name }}</h2>
        <p>Temperature: {{ weather.main.temp }} °C</p>
        <p>Condition: {{ weather.weather[0].description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
// 28:31 - Библиотека axios
import axios from 'axios';

export default {
  data() {
    return {
      // 09:00 - Переменные
      city: '',
      weather: null,
      errorMessage: '',
    };
  },
  // 19:54 - Computed свойства
  computed: { //Вычисление значение на основен других данных компонента
    apiUrl() {
      return `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=your_api_key`;
    },
  },
  methods: {
    // 21:38 - Создание методов
    async fetchWeather() {
      // 11:33 - Обработчики событий
      try {
        const response = await axios.get(this.apiUrl);
        // 26:24 - Получение погоды
        this.weather = response.data;
        this.errorMessage = '';
		console.log("Привет мир)";
      } catch (error) {
        this.errorMessage = 'City not found. Please try again.';
        this.weather = null;
      }
    },
  },
};
</script>

<!-- 00:35 - Подключение стилей -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

input {
  padding: 10px;
  font-size: 16px;
  margin-bottom: 10px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
}

h2 {
  margin: 20px 0 10px;
}

p {
  margin: 5px 0;
}
</style>
