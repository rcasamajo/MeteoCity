<template>
    <div class="column">
        <div class="tile box notification is-warning is-size-6">
            <div>
                <h3>Forecast</h3>
                <br/>
                ({{ city }})
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "CityForecast",
        props: ['city']
    }
</script>

<style scoped>

</style>