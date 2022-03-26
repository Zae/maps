<template>
    <l-map
        class="map"
        :zoom="zoom"
        :center="center"
        :bounds="bounds"
        :options="options"
        style="height: 100%;"
    >
        <l-tile-layer
            :url="url"
            :attribution="attribution"
            layer-type="base"
        />
    </l-map>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";

export default  {
    components: {
        LMap,
        LTileLayer,
    },
    data() {
        return {
            zoom: 13.2,
            center: [52.375103, 4.890201],
            bounds: null,
            url: 'https://tiles.thesonicdeathmonkeyexperience.nl/{z}/{x}/{y}.png',
            attribution: '&copy; <a href="https://osm.org/copyright">OpenStreetMap</a> contributors',
            currentZoom: 15,
            currentCenter: [52.375103, 4.890201],
            options: {
                zoomSnap: 0.5,
                maxZoom: 15
            }
        };
    },
}
</script>

<style scoped>
.map {
    width: 100vw;
    height: 100vh;
    position: absolute;
    left: 0;
    top: 0;
}
</style>
