<template>
    <div>
        <!-- a simple list group made with bootstrap that uses props that were recieved from app.vue and displays/updates data -->
        <ul class="list-group">
            <li class="list-group-item">City: {{city}}</li>
            <li class="list-group-item">Temperature: {{temp}} {{type}}</li>
            <li class="list-group-item">Conditions: {{condition}}</li>
            <li class="list-group-item"><img v-bind:src="conditionImg"></li>
        </ul>
    </div>
</template>

<script>
//Dylan Daniels 
//CIS 131
//12/11/2020
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