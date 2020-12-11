<template>
    <div>
        <!-- a bunch of bootstrap styling, but creates an input that allows the user to type in a zip code and check a radio box -->
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text" id="inputGroup-sizing-default">Zip Code:</span>
            </div>
            <input type="text" v-model="zip" placeholder="Input Zip Code" class="form-control" aria-label="Default" aria-describedby="inputGroup-sizing-default" name="zip">
            <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="button" v-on:click="logit">Submit</button>
            </div>
        </div>
        <div class="form-check">
            <input v-on:click="tempCheck" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1" checked>
            <label class="form-check-label" for="flexRadioDefault1">
                Fahrenheit
            </label>
        </div>
        <div class="form-check">
            <input v-on:click="tempCheck" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2">
            <label class="form-check-label" for="flexRadioDefault2">
                Celsius
            </label>
        </div>
    </div>
</template>

<script>
//Dylan Daniels 
//CIS 131
//12/11/2020
export default {
    name:"ZipCode",
    data: function() {
        return{
            zip:"",
            zipCode:"",
            ready: false,
            fahren: true,
            celsius: false,
            zipCheck: /^\d{5}(-\d{4})?(?!-)$/
        }
        //uses a regular expression to check to make sure the user has input is in zip code format
    },
    methods: {
        //checks our zip and continues if it passes and tells them that is it not valid otherwise, axious is not called
        logit: function() {
            if(this.zipCheck.test(this.zip))
            {
                this.zipCode = this.zip;
                this.$emit("updateWeather", this.zipCode);
                console.log(this.zipCode);
                this.zip ="";
                this.ready = true;
            }
            else{
                document.getElementsByName('zip')[0].value="";
                document.getElementsByName('zip')[0].placeholder = "Please enter a 5 digit ZIP code, Ex:12345";
            }


        },
        tempCheck()
        //checks radio boxes before firing event for our methods in the app.vue
        {

            if(this.ready)
            {
                if(document.getElementById('flexRadioDefault1').checked)
                {
                    this.$emit("updateTemp", this.fahren);
                }
                else if(document.getElementById('flexRadioDefault2').checked)
                {
                    this.$emit("updateTemp", this.celsius);
                }
            }
        }
    }
}
</script>

<style scoped>
    
</style>