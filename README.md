# Weather-App
This a Weather App
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }

        .weather-container {
            text-align: center;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            background-color: #fff;
        }

        h1 {
            margin-top: 0;
        }
    </style>
</head>

<body>
    <div class="weather-container">
        <h1>Weather App</h1>
        <div>
            <label for="city">Enter City:</label>
            <input type="text" id="city" placeholder="Enter city name">
            <button onclick="getWeather()">Get Weather</button>
        </div>
        <div id="weather-info"></div>
    </div>

    <script>
        function getWeather() {
            const city = document.getElementById('city').value;
            const apiKey = 'YOUR_API_KEY'; // Replace with your OpenWeatherMap API key
            const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

            fetch(url)
                .then(response => response.json())
                .then(data => {
                    const weatherInfo = document.getElementById('weather-info');
                    if (data.cod === 200) {
                        const { name, main, weather } = data;
                        const { temp, humidity } = main;
                        const weatherDescription = weather[0].description;

                        const weatherHTML = `
                            <h2>${name}</h2>
                            <p>Temperature: ${temp}°C</p>
                            <p>Humidity: ${humidity}%</p>
                            <p>Description: ${weatherDescription}</p>
                        `;
                        weatherInfo.innerHTML = weatherHTML;
                    } else {
                        weatherInfo.innerHTML = `<p>City not found</p>`;
                    }
                })
                .catch(error => {
                    console.log('Error fetching weather data:', error);
                });
        }
    </script>
</body>

</html>
