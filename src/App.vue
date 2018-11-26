<template>
  <div id="app">
    <h1 class="title container">City Weather</h1>
    <CitysInfo v-bind:llista-ciutats="europa"></CitysInfo>
    <CitysInfo v-bind:llista-ciutats="asia"></CitysInfo>
  </div>
</template>

<script>
import CitysInfo from "./components/CitysInfo";

export default {
    name: 'app',
    data () {
        return {
            europa: [
                "Barcelona",
                "Lleida",
                "Zaragoza",
                "Sevilla",
                "Madrid",
                "Vigo",
                "Paris",
                "Amsterdam"],
            asia: [
                "Pekin",
                "Tokyo",
                "Hong Kong",
                "Shangai",
                "Hanoi"],
            america: [
                "New York",
                "Buenos Aires",
                "Lima",
                "Los Angeles",
                "Bogota"]
        }
    },
    components: {CitysInfo}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
