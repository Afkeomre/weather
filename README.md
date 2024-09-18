# 🔆 Weather Search Application 

This is a simple weather search application that allows users to input a city name and receive the current weather conditions for that location. The user interface is designed with a responsive layout and includes a search bar, error messages for invalid inputs, and a visual display of the weather data.

## 🌐 Website 
You can try the Weather Search Application online [here](https://afkeomre.github.io/weather/).

## ✔️ Features 

- **Search Functionality**: the app allows users to enter the name of a city to search for current weather conditions.
- **Weather Display**: displays the current temperature, weather conditions, location, and date.
- **Error Handling**: shows an error message if the search input is invalid or if the location cannot be found.
- **Dynamic Themes**: the website automatically changes the background image and button color based on the temperature. There are two themes: a "cold" theme for low temperatures and a "warm" theme for higher temperatures.
- **Responsive Design**: the layout adjusts to different screen sizes, ensuring a smooth user experience on both desktop and mobile devices.

## 👀 Preview 

### 🖥️ Desktop 

| ![Main Screen](public/screenshots/main-screen.jpg) | ![Warm Theme](public/screenshots/warm-theme.jpg) |
|:--:|:--:|
| Main screen | Warm theme |

| ![Cold Theme](public/screenshots/cold-theme.jpg) | ![Error Message](public/screenshots/error-message.jpg) |
|:--:|:--:|
| Cold theme | Error message |


### 📱 Mobile devices 
| ![Main Screen Mobile](public/screenshots/main-screen-mobile.jpg) | ![Warm Theme Mobile](public/screenshots/warm-theme-mobile.jpg) | ![Cold Theme Mobile](public/screenshots/cold-theme-mobile.jpg) | ![Error Message Mobile](public/screenshots/error-messsage-mobile.jpg) |
|:--:|:--:|:--:|:--:|
| Main screen | Warm theme | Cold theme | Error message |

## 🛠 Technologies Used
- **Vue.js**: This project is built using Vue.js, a popular JavaScript framework for building user interfaces. Vue.js is known for its simplicity and flexibility, making it a great choice for developing responsive and interactive web applications like this weather search app.
- **OpenWeatherMap API**: The weather data is fetched from the OpenWeatherMap API. OpenWeatherMap provides a robust and easy-to-use API that offers weather information such as temperature, humidity, wind speed, and more. This API is free to use (with limits) and supports weather data retrieval for cities worldwide, making it ideal for real-time weather updates in this application.
To learn more about the OpenWeatherMap API, visit [their official website](https://openweathermap.org/).

## ⚙️ Project setup 
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
