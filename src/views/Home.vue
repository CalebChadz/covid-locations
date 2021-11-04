<template>
<div class="home">
  <l-map style="height:50vh">
    <l-geo-json :geojson="geojson" />
  </l-map>
</div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import {
LMap, LGeoJson
} from "@vue-leaflet/vue-leaflet";

export default {
  name: 'Home',
  components: {
    LMap,
    LGeoJson,
  },
  setup(){
    //request the geoJSOn from ministry website "https://raw.githubusercontent.com/minhealthnz/nz-covid-data/main/locations-of-interest/august-2021/locations-of-interest.geojson"
    const LOIURL = 'https://raw.githubusercontent.com/minhealthnz/nz-covid-data/main/locations-of-interest/august-2021/locations-of-interest.geojson';
    async function getProviders() {
      //request the geojson store into response.
      const response = await fetch(LOIURL);
      const geoJsonText = await response.text();
      const geojson = {
        geojson: {

        },
        geojsonOptions: {

        },
      };
      geojson.geojson = JSON.parse(geoJsonText);
      console.log(geojson);
      return geojson;
    }
    return getProviders(); 
  },
  async beforeMount() {
  // HERE is where to load Leaflet components!
  const { circleMarker } = await import("leaflet/dist/leaflet-src.esm");

  // And now the Leaflet circleMarker function can be used by the options:
  this.geojsonOptions.pointToLayer = (feature, latLng) =>
    circleMarker(latLng, { radius: 8 });
  this.mapIsReady = true;
  },
};
</script>
<style lang="scss">
.home {
  width: 100%;
  height: 100%;
}
</style>
