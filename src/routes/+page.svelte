<script>
    const apiKey = "94ba61902559a7e07b3a4afc92d1696f";
    const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=berlin";
  

const searchBox = document.querySelector(".search input");
const searchBtn = document.querySelector(".search button");
    /**
     * @param {string} city
     */
async function checkWeather(city){
    const response = await fetch(apiUrl + city + `&appid=${apiKey}`);
    var data = await response.json();

// @ts-ignore
document.querySelector(".city").innerHTML = data.name
// @ts-ignore
document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°c"
// @ts-ignore
document.querySelector(".humidity").innerHTML = data.main.humidity + "%"
// @ts-ignore
document.querySelector(".wind").innerHTML = data.wind.speed + " km/h"


console.log(data)


// @ts-ignore
if(data.weather[0].main == "Clouds"){
  
  // @ts-ignore
  document.getElementById("weather-icon").src = "../img/cloud.png";

}else if(data.weather[0].main == "Clear"){

  // @ts-ignore
  document.getElementById("weather-icon").src = "../img/sun.png";

}else if(data.weather[0].main == "Rain"){

  // @ts-ignore
  document.getElementById("weather-icon").src = "../img/rain.png";
}else if(data.weather[0].main == "Snow"){

// @ts-ignore
document.getElementById("weather-icon").src = "../img/snow.png";
}


}

searchBtn?.addEventListener("click", ()=>{
    // @ts-ignore
    checkWeather(searchBox.value)
})
   

    


  
    


</script>

<div class="card     w-full h-auto flex justify-center items-center flex-col">
    <div class="search    flex justify-center items-center mt-16 border-solid border-2 rounded-lg px-5 py-2">
        <input type="text" placeholder="Enter City Name" spellcheck="false">
        <button class="bg-gray-300"><img src="../img/search.png" width="32" height="32" alt="search"></button>
    </div>



    <div class="weather d-none w-full  mt-11 flex items-center justify-center flex-col">
        <!-- svelte-ignore a11y-missing-attribute -->
        <img src="../img/" width="150" height="150" id="weather-icon">
        <h1 class="temp  mt-11 font-bold text-xl">22°c</h1>
        <h2 class="city    font-bold text-xl">New York</h2>

        <div class="detail w-full  flex justify-around gap-11 mt-32">


<!---   column 1    -->
            <div class="col     flex  justify-center items-center text-center">
                <!-- svelte-ignore a11y-missing-attribute -->
                <img src="../img/humidity.png" width="60" height="60">
                
                <div>
                    <p class="humidity">50%</p>
                    <p>Humidity</p>
                </div>
            </div>
<!---   end column 1   -->



<!---   column 2    -->
            <div class="col      flex justify-center items-center text-center">
                <!-- svelte-ignore a11y-missing-attribute -->
                <img src="../img/wind.png" width="60" height="60">
                
                <div>
                    <p class="wind">15 km/h</p>
                    <p>Wind Speed</p>
                </div>
            </div>

<!---   end column 2   -->

        </div>
    </div>
</div>