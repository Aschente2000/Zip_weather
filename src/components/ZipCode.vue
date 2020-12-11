<template>
    <div>
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
    },
    methods: {
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