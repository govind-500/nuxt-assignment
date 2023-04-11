<template>
  <div style="height: 75vh">
    <!-- Start of Leaflet map -->
    <div id="map" style="height: 100vh">
      <client-only>
        <l-map :zoom="zoom" :center="center" :use-global-leaflet="false">
          <l-tile-layer :url="mapViewUrl"></l-tile-layer>
          <l-marker :lat-lng="markerLatLng">
            <l-popup ref="popup">
              <LeafletPopup :personDetails="personDetails"></LeafletPopup>
            </l-popup>
          </l-marker>
        </l-map>
      </client-only>
    </div>
    <!-- End of Leaflet map-->
  </div>
</template>


<script setup lang="ts">
import { defineProps } from "vue";
import { LMap, LTileLayer, LMarker, LPopup } from "@vue-leaflet/vue-leaflet";

const props = defineProps({
  /**
   * The center of the map
   */
  center: {
    type: [Array, Object],
    default: () => [0, 0],
  },

  /**
   *  location marker latitude and langitude
   */
  markerLatLng: {
    type: [Array, Object],
    default: () => [0, 0],
  },

  /**
   * The zoom of the map
   */
  zoom: {
    type: Number,
    default: 13,
  },

  /**
   *  this url prop used for map view
   */
  mapViewUrl: {
    type: String,
    default: "",
  },
});

// this array for person showing in popup
const personDetails = ref([
  {
    name: "John cerea",
    imageUrl:
      "https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80",
  },
]);
</script>
