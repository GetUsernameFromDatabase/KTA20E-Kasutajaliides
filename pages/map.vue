<template>
  <div>
    <v-btn @click="center={lat: 45, lng:25}; zoom=10;">
      go to somewhere
    </v-btn>
    <google-map
      :center="center"
      :zoom="zoom"
      :marker-coordinates="markerCoordinates"
    />
  </div>
</template>

<script>
import GoogleMap from '~/components/GoogleMap.vue';

export default {
  name: 'ShowGoogleMaps',
  components: { GoogleMap },
  data(){
      return {
          center: {lat: 44, lng: 24},
          zoom: 4,
          markerCoordinates: [{lat: 45, lng:25}],
      };
  }
   
};
</script>

<style>
   
</style>