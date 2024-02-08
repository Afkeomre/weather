<template>
	<div 
		:class="weather.main?.temp >= 15 ? 'warm' : ''" 
		id="app-content"
	>
		<main>
			<form class="search-box" @submit.prevent="fetchWeather">
				<input 
					id="search"
					type="text" 
					class="search-bar" 
					placeholder="Search..."
					v-model="query"
					@input="clearLabel"
				>
				<label for="search" class="error-message">{{ error }}</label>
				<button class="btn" :class="weather.main?.temp >= 15 ? 'btn-warm' : ''" type="submit">
					<svg fill="#fff" width="50px" height="50px" viewBox="0 0 32.00 32.00" xmlns="http://www.w3.org/2000/svg" stroke="#fff" stroke-width="0.00032"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round" stroke="#CCCCCC" stroke-width="1.024"></g><g id="SVGRepo_iconCarrier"><path d="M27 24.57l-5.647-5.648a8.895 8.895 0 0 0 1.522-4.984C22.875 9.01 18.867 5 13.938 5 9.01 5 5 9.01 5 13.938c0 4.929 4.01 8.938 8.938 8.938a8.887 8.887 0 0 0 4.984-1.522L24.568 27 27 24.57zm-13.062-4.445a6.194 6.194 0 0 1-6.188-6.188 6.195 6.195 0 0 1 6.188-6.188 6.195 6.195 0 0 1 6.188 6.188 6.195 6.195 0 0 1-6.188 6.188z"></path></g></svg>
				</button>
			</form>

			<div class="weather-wrap" v-if="weather.main">
				<div class="location-box">
					<div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
					<div class="date">{{ dateBuilder }}</div>
				</div>

				<div class="weather-box">
					<div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
					<div class="weather">	{{ weather.weather[0].main }} </div>
				</div>
			</div>

			<div class="message-wrapper" v-else>
				<div class="message">Check the weather in your city!</div>
			</div>

		</main>
	</div>
</template>

<script>


export default {
  name: 'App',
  data() {
		return {
			apiKey: 'd8e2bcfe8a7f1b00604c67da0c87601f',
			urlBase: 'https://api.openweathermap.org/data/2.5/',
			query: '',
			weather: {},
			error: ''
		}
	},
	computed: {
		dateBuilder() {
			let d = new Date();
			let months = ['January', 'February', 'March', 'April', 'May', 'June',
				'July', 'August', 'September', 'October', 'November', 'December'];
			let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

			let day = days[d.getDay()];
			let date = d.getDate();
			let month = months[d.getMonth()];
			let year = d.getFullYear();

			return `${day}, ${date} ${month}, ${year}`;
		}
	},
	methods: {
		fetchWeather() {
			fetch(`${this.urlBase}weather?q=${this.query}&units=metric&APPID=${this.apiKey}`)
				.then(res => {
					if (res.status !== 404) {
						return res;
					} else {
						let error = new Error();
						throw error;
					}
				})
				.then(res => res.json())
				.then(json => {
						this.weather = json;
						this.query = '';
						this.error = '';
				})
				.catch(() => {
					this.error = 'Incorrect city name';
				})
		},
		clearLabel() {
			if (this.query === '') {
				this.error = '';
			}
		}
	} 
}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	body {
		font-family: 'Montserrat', sans-serif;
	}

	#app-content {
		background-image: url('./assets/cold-bg.jpg');
		background-size: cover;
		background-position: bottom;
		transition: 0.4s;
	}

	#app-content.warm {
		background-image: url('./assets/warm-bg.jpg');
	}

	main {
		min-height: 100vh;
		padding: 25px 15px;
		background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
	}

	.search-box {
		width: 100%;
		margin-bottom: 50px;
		position: relative;
	}

	.search-bar {
		display: block;
		width: 100%;
		height: 55px;
		padding: 15px;
		color: #313131;
		font-size: 20px;
		appearance: none;
		border: none;
		outline: none;
		background: none;
		box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
		background-color: rgba(255, 255, 255, 0.5);
		border-radius: 0 16px 0 16px;
		transition: 0.4s;
	}

	.search-bar:focus {
		box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
		background-color: rgba(255, 255, 255, 0.75);
	}

	.error-message {
		color: red;
		font-size: 14px;
		padding-left: 8px;
		padding-top: 6px;
	}

	.btn {
		background-color: #2a8a7f;
		border-radius: 0 16px 0 0;
		height: 55px;
		position: absolute;
		right: 0;
		top: 0;
		overflow: hidden;
		border: none;
		box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
	}

	.btn:hover {
		background-color: #27695a;
		box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
	}

	.btn-warm {
		background-color: #b64d6b;
	}

	.btn-warm:hover {
		background-color: #8a364e;
	}

	.location-box,
	.weather-box {
		color: #fff;
		text-align: center;
		margin-bottom: 30px;
	}

	.location {
		font-size: 32px;
		font-weight: 500;
		text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
	}

	.date {
		font-size: 20px;
		font-weight: 300;
		font-style: italic;
	}

	.temp {
		display: inline-block;
		padding: 10px 15px;
		font-size: 96px;
		font-weight: 900;
		text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
		background-color: rgba(255, 255, 255, 0.25);
		border-radius: 16px;
		margin-bottom: 30px;
		box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	}

	.weather {
		font-size: 48px;
		font-weight: 700;
		font-style: italic;
		text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	}

	.message-wrapper {
		color: #fff;
		font-size: 52px;
		padding: 80px 10px 10px;
		text-align: center;
		font-weight: 700;
		text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
	}
</style>
