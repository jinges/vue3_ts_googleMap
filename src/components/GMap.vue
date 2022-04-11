<template>
  <div class="map" ref="mapDivRef"></div>
</template>

<script>
import { ref, onMounted, watch } from "vue";

export default {
  name: "GMap",
  props: {
    center: { lat: Number, lng: Number },
    zoom: Number,
    mapType: String,
    disableUI: Boolean,
    start: { lat: Number, lng: Number },
    end: { lat: Number, lng: Number },
    waypoints: []
  },
  setup(props) {
    // the google map object
    const map = ref(null);

    // the map element in the templste
    const mapDivRef = ref(null);

    // load in the google script
    onMounted(() => {
      // key is is the .env file
      const key = 'AIzaSyCELFoswhkJturS-o1RMRA8IdeoUGCYulE';
      // create the script element to load
      const googleMapScript = document.createElement("SCRIPT");
      googleMapScript.setAttribute(
        "src",
        `https://maps.googleapis.com/maps/api/js?key=${key}&callback=initMap`
      );
      googleMapScript.setAttribute("defer", "");
      googleMapScript.setAttribute("async", "");
      document.head.appendChild(googleMapScript);
    });

    

    function loadDirection() {
      const directionsService = new window.google.maps.DirectionsService();
      const directionsRenderer = new window.google.maps.DirectionsRenderer();

      directionsRenderer.setMap(map.value);

      calculateAndDisplayRoute(directionsService, directionsRenderer);
    }

    function calculateAndDisplayRoute(directionsService ,directionsRenderer) {
      
    console.log(props.start);
      directionsService
        .route({
          origin:  props.start,
          destination:  props.end,
          waypoints:props.waypoints,
          travelMode: window.google.maps.TravelMode.DRIVING,
        })
        .then((response) => {
          directionsRenderer.setDirections(response);
        })
        .catch((e) => window.alert("Directions request failed due to " + status));
    }


    /**
     * this function is called as soon as the map is initialized
     */
    window.initMap = () => {
      map.value = new window.google.maps.Map(mapDivRef.value, {
        mapTypeId: props.mapType || "hybrid",
        zoom: props.zoom || 8,
        disableDefaultUI: props.disableUI || false,
        center: props.center || { lat: 38.0, lng: -77.01 }
      });
      
      loadDirection(props)
    };

    watch(
      () => props.start,
      (start, oldStart) =>{
        console.log(start, oldStart);
      }
    );
    return {
      mapDivRef
    };
  }

  
};
</script>

<style lang="css" scoped>
.map {
  width: 100%;
  height: 300px;
  background-color: azure;
}
</style>