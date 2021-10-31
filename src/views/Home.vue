<template>
  <div class="home">
    <l-map :center="[47.41322, -1.219482]">
       <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></l-tile-layer>
      <l-control-layers />
    </l-map>
  </div>
</template>

<script>
// @ is an alias to /src
import {
  LMap,  
  LTileLayer,
  LMarker,
  LControlLayers,
} from "@vue-leaflet/vue-leaflet";

export default {
  name: 'Home',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LControlLayers,
  },
};
</script>
<style lang="scss">
.home {
  width: 100%;
  height: 100%;
}
</style>
