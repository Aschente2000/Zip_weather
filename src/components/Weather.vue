<template>
    <div>
        <!-- <p>temp: {{temp}} {{type}}</p>
        <p>conditions: </p>
        <img v-bind:src="condition">
        <p>city: {{city}}</p> -->
        <ul class="list-group">
            <li class="list-group-item">City: {{city}}</li>
            <li class="list-group-item">Temperature: {{temp}} {{type}}</li>
            <li class="list-group-item">Conditions: {{condition}}</li>
            <li class="list-group-item"><img v-bind:src="conditionImg"></li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "Weather",
    props:['city','condition', 'conditionImg', 'temp', 'type']

}
</script>

<style scoped>
    *{
        color: black;
    }
</style>