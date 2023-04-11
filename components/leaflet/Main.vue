<template>
  <div>
    <LeafletList
      :center="center"
      :markerLatLng="markerLatLng"
      :zoom="zoom"
      :mapViewUrl="mapViewUrl"
    ></LeafletList>
  </div>
</template>
<script lang="ts" setup>
import { ref } from "vue";

// declaring variables are passing through the props

const center = ref([17.4484363, 78.3741361]);
const markerLatLng = ref([17.4484363, 78.3741361]);
const zoom = ref(13);
const mapViewUrl = ref("https://{s}.tile.osm.org/{z}/{x}/{y}.png");
</script>
