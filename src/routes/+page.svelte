<script lang="ts">
    const apiKey = "94ba61902559a7e07b3a4afc92d1696f";
    const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

    const weatherIcons = {
        '01d': '../img/sun.png',
        '01n': '../img/moon.png',
        '02d': '../img/sun-cloud.png',
        '02n': '../img/moon-cloud.png',
        '03d': '../img/cloud.png',
        '03n': '../img/cloud.png',
        '04n': '../img/more-cloud.png',
        '04d': '../img/more-cloud.png',
        '10d': '../img/rain.png',
        '10n': '../img/rain.png',
        '11n': '../img/storm.png',
        '11d': '../img/storm.png',
        '13n': '../img/snow.png',
        '13d': '../img/snow.png',
        '50d': '../img/dust.png',
        '50n': '../img/dust.png',
        // Add more mappings for other weather conditions as needed
    };

    let data = {
        NamePlace: " ",
        temperature: "هیچ گەڕانێک ئەنجام نەدراوە",
        humidity: "0",
        windSpeed: "0",
        weatherIcon: " ",
    };

    /**
     * @param {string} city
     */
    async function checkWeather(city: string) {
        try {
            const response = await fetch(apiUrl + city + `&appid=${apiKey}`);
            const apiData = await response.json();

            const weatherCondition = apiData.weather[0].icon;
            // @ts-ignore
            document.getElementById('weather-icon').src = `https://openweathermap.org/img/w/${weatherIcons}.png`;
            data = {
                NamePlace: apiData.name,
                temperature: Math.round(apiData.main.temp) + "°C",
                humidity: apiData.main.humidity + "%",
                windSpeed: apiData.wind.speed + " km/h",
                // @ts-ignore
                weatherIcon: weatherIcons[weatherCondition] || " ",
                
            };
        } catch (error) {
            console.error("Error fetching data:", error);
        }
        
    }

    function search() {
        const cityInput = document.querySelector('input');
        // @ts-ignore
        const city = cityInput.value;
        if (city) {
            checkWeather(city);
        }
    }

</script>

<div class="card w-full h-auto flex justify-center items-center flex-col">
    <div class="search w-full flex justify-center items-center border-solid border-2 rounded-lg px-5 py-2 bg-gray-700">
        <input type="text" style="font-family: kurdish;" placeholder="بەدوای شاردا بگەڕێ" class="w-80 rounded-lg px-4 py-2 text-center" spellcheck="false">
        <button class="bg-gray-300 rounded-lg w-11 h-11 flex items-center justify-center" on:click={search}>
            <img src="../img/search.png" width="26" height="26" alt="search">
        </button>
    </div>

    <img id="weather-icon" class="mt-11" width="150" height="150" alt="Weather Icon" src={data.weatherIcon}>
    <h1 class="temp mt-11 font-bold text-xl" style="font-family: kurdish;">{data.temperature}</h1>
    <h2 class="city font-bold text-xl">{data.NamePlace}</h2>
    <div class="w-full flex justify-around gap-11 mt-32 bg-gray-300 py-4">
        <div class="flex justify-center items-center text-center ">
            <img src="../img/humidity.png" width="60" height="60" alt="Humidity Icon">
            <div>
                <p class="humidity">{data.humidity}</p>
                <p style="font-family: kurdish;">ڕێژەی شێ</p>
            </div>
        </div>
        <div class="flex justify-center items-center text-center">
            <img src="../img/wind.png" width="60" height="60" alt="Wind Icon">
            <div>
                <p class="wind">{data.windSpeed}</p>
                <p style="font-family: kurdish;">خێرایی با</p>
            </div>
        </div>
    </div>
 
</div>

<footer class="w-full h-44 flex justify-center items-center bg-gray-800 text-white">
    <p style="font-family: kurdish;">ئەم وێبسایتە دروستکراوە لەلایەن: دانا سەرکەوت محمد</p>
</footer>
