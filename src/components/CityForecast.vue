<template>
    <div class="column">
        <h3>Forecast</h3>
        <div class="tile box notification is-warning is-size-6">

            <div class="control">
                <label class="radio" v-for="n in 5">
                    <input type="radio" v-bind:value="n" v-model="dia">
                    {{ n }} day
                </label>
            </div>

            <div v-if="forecast != null" class="field">
                <br>
                <img v-bind:src="icon" alt="icon" class="image">
                <br>
                {{ forecast[(dia*8)-1].dt_txt }}
                <br/>
                {{ forecast[(dia*8)-1].main.temp }}
                <br/>
                {{ forecast[(dia*8)-1].main.humidity }}
                <br/>
                {{ forecast[(dia*8)-1].weather[0].description }}
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
                dia: "1"
            }
        },

        methods: {
            crida(ciutat) {
                var url = "https://api.openweathermap.org/data/2.5/forecast?q=" + ciutat + "&units=metric&lang=ca&appid=644da4f2a1231c6611d2e2d8abb1fc90";

                this.$http.get(url)
                    .then(response => {
                        return response.json();
                    })
                    .then(data => {
                        this.forecast = data.list;
                    })
            }
        },

        created: function () {
            this.crida(this.city);
        },

        computed: {
            icon(){
                return "http://openweathermap.org/img/w/" + this.forecast[(this.dia*8)-1].weather[0].icon + ".png";
            }
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