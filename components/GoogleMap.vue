<template>
  <div ref="map" />
</template>

<script>
import { Loader } from '@googlemaps/js-api-loader';

function addMarker(location, map) {
  // https://developers.google.com/maps/documentation/javascript/markers#marker_labels
  // eslint-disable-next-line no-undef
  const marker = new google.maps.Marker({
    position: location,
    map: map,
  });

  // https://developers.google.com/maps/documentation/javascript/infowindows#open
  marker.addListener('click', () => {
    // https://developers.google.com/maps/documentation/javascript/markers#remove
    marker.setMap(null);
  });

  return marker;
}

export default {
  name: 'GoogleMaps',
  props: {
    center: { type: Object, required: true },
    zoom: { type: Number, default: 4 },
    markerCoordinates: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      map: null,
      markers: [],
    };
  },
  watch: {
    center(newCenter) {
      this.map.panTo(newCenter);
    },
    zoom(newZoom) {
      this.map.setZoom(newZoom);
    },
  },
  mounted() {
    const loader = new Loader({
      apiKey: this.$config.googleApiKey,
      version: 'weekly',
    });

    loader.load().then((google) => {
      this.map = new google.maps.Map(this.$refs['map'], {
        center: this.center,
        zoom: this.zoom,
      });
      this.markers = this.markerCoordinates.map((coord) =>
        addMarker(coord, this.map)
      );

      google.maps.event.addListener(this.map, 'click', (event) => {
        this.markers.push(addMarker(event.latLng, this.map));
      });
    });
  },
};
</script>

<style scoped>
div {
  height: 800px;
}
</style>
