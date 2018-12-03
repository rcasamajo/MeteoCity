<template>
    <div class="column">
        <div class="tile box notification is-info is-size-6">
            <h3>Current Weather</h3>
            <div v-if="ciutatActual != null">
                {{ ciutatActual.name }}
                <br>
                {{ ciutatActual.weather[0].description }}
                <br>
                {{ ciutatActual.main.temp }}
                <br>
                {{ ciutatActual.main.pressure }}
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CityCurrentWeather",
        props:['city'],

        data () {
            return {
                ciutatActual: null,
            }
        },

        methods: {
            async crida(ciutat) {
                var url = 'https://api.openweathermap.org/data/2.5/weather?q=' + ciutat + '&units=metric&lang=ca&appid=644da4f2a1231c6611d2e2d8abb1fc90';

                try {
                    var response = await fetch(url);
                    var data = await response.json();

                    this.ciutatActual = data;
                }
                catch(err) {
                    this.console.log(err);
                }
            }
        },

        created: function () {
            this.crida(this.city);
        },

        watch: {
            city: function(value){
                this.crida(value);
            }
        }
    }
</script>

<style scoped>

</style>