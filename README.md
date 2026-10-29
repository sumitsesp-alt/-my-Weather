 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Sumit | My Personal Website</title>

    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        html {
            scroll-behavior: smooth;
        }

        body {
            font-family: Arial, sans-serif;
            background: #f1f5f9;
            color: #1e293b;
            line-height: 1.7;
        }

        header {
            background: linear-gradient(135deg, #0f172a, #1d4ed8);
            color: white;
            text-align: center;
            padding: 65px 20px;
        }

        header h1 {
            font-size: 38px;
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Weather App</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #102b55, #168aad, #52b69a);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    color: white;
}

.app {
    width: 100%;
    max-width: 390px;
    padding: 25px;
    border-radius: 25px;
    background: rgba(255, 255, 255, 0.14);
    border: 1px solid rgba(255, 255, 255, 0.25);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
    text-align: center;
}

h1 {
    margin-top: 0;
    font-size: 28px;
}

.subtitle {
    color: #e0f2fe;
    font-size: 14px;
}

.search {
    display: flex;
    gap: 8px;
    margin: 22px 0;
}

input {
    min-width: 0;
    flex: 1;
    padding: 13px;
    border: none;
    border-radius: 12px;
    outline: none;
    font-size: 15px;
}

button {
    border: none;
    border-radius: 12px;
    padding: 12px;
    background: #fef08a;
    color: #17324d;
    font-weight: bold;
    cursor: pointer;
}

#searchBtn {
    min-width: 76px;
}

.weather-icon {
    font-size: 65px;
    margin: 10px 0;
}

.temperature {
    font-size: 55px;
    font-weight: bold;
    margin: 5px;
}

#description {
    font-size: 19px;
    margin-bottom: 8px;
}

#cityName {
    font-size: 21px;
    font-weight: bold;
}

.details {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-top: 25px;
}

.detail {
    background: rgba(255, 255, 255, 0.14);
    border-radius: 15px;
    padding: 15px 5px;
}

.detail p {
    margin: 5px;
}

.value {
    font-size: 19px;
    font-weight: bold;
}

#message {
    min-height: 20px;
    font-size: 14px;
    color: #fff7ae;
}

footer {
    margin-top: 20px;
    font-size: 12px;
    color: #e0f2fe;
}

footer a {
    color: white;
}
</style>
</head>

<body>

<div class="app">
    <h1>🌦️ Weather App</h1>
    <p class="subtitle">Check the weather in your city</p>

    <form class="search" id="searchForm">
        <input
            type="text"
            id="cityInput"
            placeholder="Enter city name"
            value="Solapur"
            required
        >
        <button id="searchBtn" type="submit">Search</button>
    </form>

    <p id="message" role="status">Search for a city!</p>

    <div class="weather-icon" id="icon">🌤️</div>
    <div id="cityName">Weather</div>
    <div class="temperature" id="temperature">--°C</div>
    <p id="description">Weather condition</p>
    <p id="feelsLike">Feels like: --°C</p>

    <div class="details">
        <div class="detail">
            <p>💧 Humidity</p>
            <p class="value" id="humidity">--%</p>
        </div>

        <div class="detail">
            <p>💨 Wind Speed</p>
            <p class="value" id="wind">-- km/h</p>
        </div>

        <div class="detail">
            <p>🌧️ Rain</p>
            <p class="value" id="rain">-- mm</p>
        </div>

        <div class="detail">
            <p>☁️ Cloud Cover</p>
            <p class="value" id="cloud">--%</p>
        </div>
    </div>

    <footer>
        Weather data by
        <a href="https://open-meteo.com/" target="_blank">
            Open-Meteo
        </a>
    </footer>
</div>

<script>
const form = document.getElementById("searchForm");
const input = document.getElementById("cityInput");
const message = document.getElementById("message");
const searchBtn = document.getElementById("searchBtn");

function getWeatherInfo(code) {
    if (code === 0) return ["☀️", "Clear sky"];
    if ([1, 2, 3].includes(code)) return ["🌤️", "Partly cloudy"];
    if ([45, 48].includes(code)) return ["🌫️", "Foggy"];
    if ([51, 53, 55, 56, 57].includes(code))
        return ["🌦️", "Drizzle"];
    if ([61, 63, 65, 66, 67, 80, 81, 82].includes(code))
        return ["🌧️", "Rainy"];
    if ([71, 73, 75, 77, 85, 86].includes(code))
        return ["❄️", "Snowy"];
    if ([95, 96, 99].includes(code))
        return ["⛈️", "Thunderstorm"];

    return ["🌡️", "Weather conditions"];
}

async function searchWeather(city) {
    if (!city.trim()) {
        message.textContent = "Please enter a city name.";
        return;
    }

    searchBtn.disabled = true;
    searchBtn.textContent = "...";
    message.textContent = "Loading weather data...";

    try {
        const geoUrl =
            "https://geocoding-api.open-meteo.com/v1/search?name=" +
            encodeURIComponent(city) +
            "&count=1&language=en&format=json";

        const geoResponse = await fetch(geoUrl);

        if (!geoResponse.ok) {
            throw new Error("Could not search for the city.");
        }

        const geoData = await geoResponse.json();

        if (!geoData.results || geoData.results.length === 0) {
            throw new Error("City not found. Check the spelling.");
        }

        const place = geoData.results[0];

        const weatherUrl =
            "https://api.open-meteo.com/v1/forecast" +
            "?latitude=" + place.latitude +
            "&longitude=" + place.longitude +
            "&current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,weather_code,cloud_cover,wind_speed_10m" +
            "&timezone=auto";

        const weatherResponse = await fetch(weatherUrl);

        if (!weatherResponse.ok) {
            throw new Error("Weather data is unavailable.");
        }

        const weatherData = await weatherResponse.json();
        const current = weatherData.current;

        const info = getWeatherInfo(current.weather_code);

        document.getElementById("cityName").textContent =
            place.name +
            (place.admin1 ? ", " + place.admin1 : "") +
            (place.country ? ", " + place.country : "");

        document.getElementById("icon").textContent =
            current.is_day === 0 && current.weather_code === 0
                ? "🌙"
                : info[0];

        document.getElementById("temperature").textContent =
            Math.round(current.temperature_2m) + "°C";

        document.getElementById("description").textContent = info[1];

        document.getElementById("feelsLike").textContent =
            "Feels like: " +
            Math.round(current.apparent_temperature) + "°C";

        document.getElementById("humidity").textContent =
            current.relative_humidity_2m + "%";

        document.getElementById("wind").textContent =
            current.wind_speed_10m + " km/h";

        document.getElementById("rain").textContent =
            current.precipitation + " mm";

        document.getElementById("cloud").textContent =
            current.cloud_cover + "%";

        message.textContent =
            "Updated: " + current.time.replace("T", " ");

    } catch (error) {
        message.textContent =
            error.message ||
            "Something went wrong. Please try again.";
    } finally {
        searchBtn.disabled = false;
        searchBtn.textContent = "Search";
    }
}

form.addEventListener("submit", function(event) {
    event.preventDefault();
    searchWeather(input.value);
});

searchWeather(input.value);
</script>
</body>
</html>

</body>
</html>
