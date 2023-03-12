<template>
    <form>
        <v-text-field
            v-model="vrm"
            label="VRM"
            prepend-inner-icon="mdi-car"
            required
        ></v-text-field>

        <v-text-field
            v-model="forceNumber"
            label="Force Number"
            prepend-inner-icon="mdi-badge-account"
            required
        ></v-text-field>

        <v-checkbox
            v-model="saveForceNumber"
            label="Save Force Number"
        ></v-checkbox>

        <v-text-field
            v-model="location"
            label="Location"
            prepend-inner-icon="mdi-map-marker"
            :readonly="autoLocation"
            :loading="locationLoading"
            required
        ></v-text-field>

        <v-btn
            v-on:click="getLocation"
        >Get Location</v-btn>

        <v-btn

        >Submit</v-btn>
    </form>
  </template>
  
<script lang="ts">
    export default {
        data() {
            return {
                vrm: "",
                forceNumber: "",
                saveForceNumber: false,
                autoLocation: false,
                location: "",
                locationLoading: false,
            }
        },
        methods: {
            getLocation() {
                let success = (position : any) => {
                    this.autoLocation = true;
                    this.locationLoading = false;
                    const latitude = position.coords.latitude;
                    const longitude = position.coords.longitude;
                    this.location = latitude + ", " + longitude;
                }

                let error = () => {
                    this.autoLocation = false;
                    this.locationLoading = false;
                }

                if (!navigator.geolocation) {
                    this.autoLocation = false;
                } else {
                    navigator.geolocation.getCurrentPosition(success, error);
                    this.locationLoading = true;
                }
            }
        },
        mounted() {
            this.getLocation()
        }
    }

</script>