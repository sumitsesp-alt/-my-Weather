<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Weather - Sumit</title>

<style>
* {
    box-sizing: border-box;
}

body {
    margin: 0;
    font-family: Arial, sans-serif;
    color: #202536;
    background: linear-gradient(180deg, #d9e9ff, #f4f7fc);
    min-height: 100vh;
    padding: 22px 12px;
}

.app {
    max-width: 760px;
    margin: auto;
}

.top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 12px;
    margin-bottom: 18px;
}

h1 {
    margin: 0;
    font-size: 27px;
}

.small {
    color: #65738b;
    font-size: 13px;
    margin-top: 6px;
}

.search {
    display: flex;
    gap: 7px;
    margin-bottom: 16px;
}

input {
    flex: 1;
    min-width: 0;
    border: 1px solid #dce4f0;
    border-radius: 24px;
    padding: 14px 17px;
    font-size: 16px;
    background: white;
}

button {
    border: none;
    border-radius: 22px;
    padding: 12px 18px;
    font-size: 14px;
    font-weight: bold;
    cursor: pointer;
    background: #2463eb;
    color: white;
}

button:disabled {
    opacity: 0.6;
}

.card {
    background: rgba(255,255,255,0.94);
    border-radius: 23px;
    padding: 20px;
    margin-bottom: 15px;
    box-shadow: 0 5px 22px rgba(36, 65, 110, 0.07);
}

.label {
    color: #69758a;
    font-size: 14px;
}

.current {
    background: linear-gradient(130deg, #ffffff, #e8f2ff);
}

.main-weather {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    margin: 16px 0 22px;
}

.temp {
    font-size: 66px;
    font-weight: 700;
    letter-spacing: -3px;
}

.icon {
    font-size: 65px;
}

.condition {
    font-size: 18px;
    font-weight: bold;
}

.city {
    font-size: 21px;
    font-weight: bold;
    margin-top: 8px;
}

.feels {
    color: #66738a;
    margin-top: 7px;
    font-size: 14px;
}

.section-title {
    font-size: 19px;
    font-weight: bold;
    margin-bottom: 16px;
}

.hourly {
    display: flex;
    overflow-x: auto;
    gap: 12px;
    padding-bottom: 7px;
}

.hour {
    flex: 0 0 74px;
    text-align: center;
    background: #f3f7fd;
    border-radius: 16px;
    padding: 13px 6px;
}

.hour-time {
    font-size: 12px;
    color: #65738b;
}

.hour-icon {
    font-size: 28px;
    margin: 13px 0;
}

.hour-temp {
    font-weight: bold;
    font-size: 15px;
}

.days {
    display: grid;
    gap: 0;
}

.day {
    display: grid;
    grid-template-columns: 1fr 40px 50px 65px;
    align-items: center;
    gap: 6px;
    padding: 12px 0;
    border-bottom: 1px solid #edf0f5;
    font-size: 14px;
}

.day:last-child {
    border-bottom: none;
}

.day-icon {
    font-size: 25px;
    text-align: center;
}

.day-range {
    text-align: right;
    font-weight: bold;
}

.details {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
}

.detail {
    background: #f4f7fc;
    border-radius: 16px;
    padding: 15px;
}

.detail-name {
    color: #69758a;
    font-size: 13px;
}

.detail-value {
    font-size: 23px;
    font-weight: bold;
    margin-top: 9px;
}

.message {
    color: #53647d;
    font-size: 13px;
    min-height: 18px;
    margin: 8px 2px 12px;
}

footer {
    text-align: center;
    color: #65738b;
    font-size: 12px;
    padding: 10px;
}

footer a {
    color: #2463eb;
}

@media (max-width: 400px) {
    .card {
        padding: 15px;
    }

    .temp {
        font-size: 55px;
    }

    .icon {
        font-size: 52px;
    }

    .day {
        grid-template-columns: 1fr 32px 43px 57px;
        font-size: 12px;
    }
}
</style>
</head>

<body>
<div class="app">

    <div class="top">
        <div>
            <h1>🌦️ Weather</h1>
            <div class="small">Weather forecast for your city</div>
        </div>
        <div style="font-size:25px">🌍</div>
    </div>

    <form class="search" id="searchForm">
        <input id="cityInput" value="Solapur"
               placeholder="Search city..." required>
        <button id="searchBtn" type="submit">Search</button>
    </form>

    <div class="message" id="message" role="status">
        Getting weather data...
    </div>

    <section class="card current">
        <div class="label">CURRENT WEATHER</div>

        <div class="main-weather">
            <div>
                <div class="temp" id="temperature">--°</div>
                <div class="condition" id="description">Loading...</div>
                <div class="city" id="cityName">Solapur</div>
                <div class="feels" id="feelsLike">Feels like --°</div>
            </div>
            <div class="icon" id="currentIcon">🌤️</div>
        </div>
    </section>

    <section class="card">
        <div class="section-title">🕒 Hourly Forecast</div>
        <div class="hourly" id="hourly">
            <div class="label">Loading hourly forecast...</div>
        </div>
    </section>

    <section class="card">
        <div class="section-title">📅 7-Day Forecast</div>
        <div class="days" id="days">
            <div class="label">Loading daily forecast...</div>
        </div>
    </section>

    <section class="card">
        <div class="section-title">Weather Details</div>
        <div class="details">
            <div class="detail">
                <div class="detail-name">💧 Humidity</div>
                <div class="detail-value" id="humidity">--%</div>
            </div>

            <div class="detail">
                <div class="detail-name">💨 Wind Speed</div>
                <div class="detail-value" id="wind">-- km/h</div>
            </div>

            <div class="detail">
                <div class="detail-name">🌧️ Rainfall</div>
                <div class="detail-value" id="rain">-- mm</div>
            </div>

            <div class="detail">
                <div class="detail-name">☁️ Cloud Cover</div>
                <div class="detail-value" id="cloud">--%</div>
            </div>
        </div>
    </section>

    <footer>
        Weather data by
        <a href="https://open-meteo.com/" target="_blank">
            Open-Meteo
        </a>
    </footer>

</div>

<script>
const $ = id => document.getElementById(id);

function weatherInfo(code, isDay = 1) {
    if (code === 0)
        return [isDay ? "☀️" : "🌙", "Clear sky"];

    if ([1, 2, 3].includes(code))
        return ["🌤️", "Partly cloudy"];

    if ([45, 48].includes(code))
        return ["🌫️", "Foggy"];

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

function dayName(date) {
    return new Date(date + "T12:00:00").toLocaleDateString(
        "en-US", { weekday: "short" }
    );
}

function hourName(date) {
    return new Date(date).toLocaleTimeString(
        "en-US", { hour: "numeric", hour12: true }
    );
}

async function searchWeather(city) {
    $("message").textContent = "Searching for " + city + "...";
    $("searchBtn").disabled = true;
    $("searchBtn").textContent = "...";

    try {
        const geoURL =
            "https://geocoding-api.open-meteo.com/v1/search?name=" +
            encodeURIComponent(city) +
            "&count=1&language=en&format=json";

        const geoResponse = await fetch(geoURL);
        if (!geoResponse.ok) throw new Error("City search failed.");

        const geoData = await geoResponse.json();

        if (!geoData.results || geoData.results.length === 0) {
            throw new Error("City not found. Check the spelling.");
        }

        const place = geoData.results[0];

        const params = new URLSearchParams({
            latitude: place.latitude,
            longitude: place.longitude,
            current: [
                "temperature_2m",
                "relative_humidity_2m",
                "apparent_temperature",
                "is_day",
                "precipitation",
                "weather_code",
                "cloud_cover",
                "wind_speed_10m"
            ].join(","),
            hourly: [
                "temperature_2m",
                "precipitation_probability",
                "weather_code"
            ].join(","),
            daily: [
                "weather_code",
                "temperature_2m_max",
                "temperature_2m_min"
            ].join(","),
            forecast_days: 7,
            timezone: "auto"
        });

        const weatherResponse = await fetch(
            "https://api.open-meteo.com/v1/forecast?" +
            params.toString()
        );
       if (!weatherResponse.ok)
            throw new Error("Could not load weather data.");

        const data = await weatherResponse.json();
        const current = data.current;

        $("cityName").textContent =
            place.name +
            (place.admin1 ? ", " + place.admin1 : "") +
            (place.country ? ", " + place.country : "");

        $("temperature").textContent =
            Math.round(current.temperature_2m) + "°";

        $("description").textContent =
            weatherInfo(current.weather_code, current.is_day)[1];

        $("currentIcon").textContent =
            weatherInfo(current.weather_code, current.is_day)[0];

        $("feelsLike").textContent =
            "Feels like " +
            Math.round(current.apparent_temperature) + "°";

        $("humidity").textContent =
            current.relative_humidity_2m + "%";

        $("wind").textContent =
            current.wind_speed_10m + " km/h";

        $("rain").textContent =
            current.precipitation + " mm";

        $("cloud").textContent =
            current.cloud_cover + "%";

        // Next 6 forecast hours
        const times = data.hourly.time;
        let index = times.findIndex(
            time => time >= current.time
        );

        if (index < 0) index = 0;

        $("hourly").innerHTML = "";

        for (let i = index; i < Math.min(index + 6, times.length); i++) {
            const info = weatherInfo(data.hourly.weather_code[i]);

            const item = document.createElement("div");
            item.className = "hour";

            const timeLabel = i === index
                ? "Now"
                : hourName(times[i]);

            item.innerHTML = `
                <div class="hour-time">${timeLabel}</div>
                <div class="hour-icon">${info[0]}</div>
                <div class="hour-temp">
                    ${Math.round(data.hourly.temperature_2m[i])}°
                </div>
                <div class="hour-time" style="margin-top:8px">
                    ${data.hourly.precipitation_probability[i] ?? 0}% rain
                </div>
            `;

            $("hourly").appendChild(item);
        }

        // 7 day forecast
        $("days").innerHTML = "";

        for (let i = 0; i < data.daily.time.length; i++) {
            const info = weatherInfo(data.daily.weather_code[i]);

            const item = document.createElement("div");
            item.className = "day";

            item.innerHTML = `
                <div>${i === 0 ? "Today" : dayName(data.daily.time[i])}</div>
                <div class="day-icon">${info[0]}</div>
                <div>${info[1]}</div>
                <div class="day-range">
                    ${Math.round(data.daily.temperature_2m_max[i])}° /
                    ${Math.round(data.daily.temperature_2m_min[i])}°
                </div>
            `;

            $("days").appendChild(item);
        }

        $("message").textContent =
            "Updated: " + current.time.replace("T", " ");

    } catch (error) {
        $("message").textContent =
            error.message + " Please check your internet and try again.";
    } finally {
        $("searchBtn").disabled = false;
        $("searchBtn").textContent = "Search";
    }
}

$("searchForm").addEventListener("submit", function(event) {
    event.preventDefault();
    searchWeather($("cityInput").value.trim());
});

searchWeather("Solapur");
</script>
</body>
</html>


