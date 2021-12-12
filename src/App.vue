<template>
    <div id="app">
        <main>
            <div class="search-box">
                <input
                    type="text"
                    class="search-box"
                    placeholder="search..."
                    v-model="query"
                    @keypress="fetchWeather"
                />
            </div>

            <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
                <div class="location-box">
                    <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
                    <div class="date">Monday 20 January 2020</div>
                </div>

                <div class="weather-box">
                    <div class="temp">{{ Math.round(weather.main.temp) }} degrees</div>
                    <div class="weather">{{ weather.weather[0].main }}</div>
                </div>
            </div>
        </main>
    </div>
</template>

<script>
export default {
    name: "app",
    data() {
        return {
            api_key: "a5766192f003e678e1f33722d141ccbb",
            url_base: "https://api.openweathermap.org/data/2.5/",
            query: "",
            weather: {},
        };
    },
    methods: {
        //only fetch if user clicks enter
        fetchWeather(e) {
            if (e.key == "Enter") {
                fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
                    .then((res) => {
                        console.log(res);
                        return res.json();
                    })
                    .then(this.setResults);
            }
        },
        setResults(results) {
            this.weather = results;
        },
        dateBuilder() {},
    },
};
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: monospace;
}

#app {
    background-image: url("./assets/cold-bg.jpeg");
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
}

main {
    min-height: 100vh;
    padding: 25px;
}

.search-box {
    width: 100%;
    margin-bottom: 30px;
}

.search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;

    color: black;
    font-size: 20px;
}

.location-box .location {
    color: black;
    font-size: 32px;
    font-weight: 500;
    text-align: center;
}

.weather-wrap {
    text-align: center;
}
</style>
