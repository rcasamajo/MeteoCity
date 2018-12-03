<template>
    <div class="column">
        <div class="tile box notification is-warning is-size-6">
            <h3>Forecast</h3>
            <div v-if="forecast != null">
                <br/>
                {{ forecast.dt_txt }}
                <br/>
                {{ forecast.main.temp }}
                <br/>
                {{ forecast.main.humidity }}
                <br/>
                {{ forecast.weather[0].description }}
                <br/>
                <img v-bind:src="icon" alt="icon" class="src">
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CityForecast",
        props: ['city'],

        data() {
            return {
                forecast: null,
                icon: ""
            }
        },

        methods: {
            crida(ciutat) {
                var url = "https://api.openweathermap.org/data/2.5/forecast?q=" + ciutat + "&units=metric&lang=ca&appid=644da4f2a1231c6611d2e2d8abb1fc90";

                this.$http.get(url)
                    .then(response => {
                        this.forecast = response.body.list[8];
                        this.icon = "http://openweathermap.org/img/w/" + response.body.list[8].weather[0].icon + ".png";
                    }, error => {
                        this.console.log(error);
                    })
            }
        },

        created: function () {
            this.crida(this.city);
        },

        watch: {
            city: function (value) {
                this.crida(value);
            }

        }
    }
</script>

<style scoped>

</style>