<template>
    <div class="column">
        <h3>Events</h3>
        <div class="tile box notification is-info is-size-6">
            <div v-if="eventsList != null">
                <ul>
                    <li v-for="event in eventsList" :key="event.id">
                        {{ event.displayName }} / <a v-bind:href="event.uri" target="_blank">+info</a>
                    </li>
                </ul>
            </div>
        </div>
    </div>

</template>

<script>
    export default {
        name: "CityEvents",
        props:['city'],

        data () {
            return {
                eventsList: null,
            }
        },

        methods: {
            async getEventsList(ciutat) {
                this.eventsList = null;
                try {
                    var url = 'https://api.songkick.com/api/3.0/search/locations.json?query=' + ciutat + '&apikey=Cglf2H7c7d4KPMO1';
                    var response = await fetch(url);
                    var data = await response.json();

                    var cityId = data.resultsPage.results.location[0].metroArea.id;

                    url = 'https://api.songkick.com/api/3.0/metro_areas/' + cityId + '/calendar.json?apikey=Cglf2H7c7d4KPMO1'
                    response = await fetch(url);
                    data = await response.json();

                    this.eventsList = data.resultsPage.results.event;
                }
                catch(err) {
                    this.console.log(err);
                }
            }
        },

        created: function () {
            this.getEventsList(this.city);
        },

        watch: {
            city: function(value){
                this.getEventsList(value);
            }
        }

    }
</script>

<style scoped>

</style>