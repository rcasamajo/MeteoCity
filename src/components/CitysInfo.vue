<template>
    <article class="container notification content is-large">
        <div class="columns">

            <div class="column is-one-quarter">
                <div class="select is-primary is-rounded is-hovered">
                    <select v-model="ciutatSelected">
                        <option v-for="city in llistaCiutats" :key="city">{{ city }}</option>
                    </select>
                </div>
            </div>

            <div class="column">
                <CityCurrentWeather v-bind:city="ciutatSelected"></CityCurrentWeather>
                <CityForecast v-bind:city="ciutatSelected"></CityForecast>
            </div>
        </div>
    </article>
</template>

<script>
    import CityCurrentWeather from "./CityCurrentWeather.vue";
    import CityForecast from "./CityForecast.vue";

    export default {
        name: "CitysInfo",
        components: {CityCurrentWeather, CityForecast},
        props:['llistaCiutats'],
        data () {
            return {
                ciutatSelected: this.llistaCiutats[0]
            }
        }
    }
</script>

<style scoped>

</style>