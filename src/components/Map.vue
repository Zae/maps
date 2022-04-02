<template>
    <l-map
        @ready="onReady"
        @locationfound="onLocationFound"
        ref="map"
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
            :max-zoom="options.maxZoom"
            :min-zoom="options.minZoom"
        />

        <template v-if="location">
            <l-circle-marker :lat-lng="location.latlng" :fillOpacity="1" :radius="0.1" />
            <l-circle-marker :lat-lng="location.latlng" :radius="location.accuracy / 2" :stroke="false" />
        </template>
    </l-map>
</template>

<script>
import "leaflet/dist/leaflet.css";
import { LMap, LTileLayer, LCircleMarker } from "@vue-leaflet/vue-leaflet";

export default  {
    components: {
        LMap,
        LTileLayer,
        LCircleMarker
    },
    data() {
        return {
            location: null,
            zoom: 13.2,
            center: [52.375103, 4.890201],
            bounds: null,
            url: 'https://maps.tsdme.workers.dev/{z}/{x}/{y}.png',
            // url: 'https://tile.thesonicdeathmonkeyexperience.nl/{z}/{x}/{y}.png',
            attribution: '&copy; <a href="https://osm.org/copyright">OpenStreetMap</a> contributors',
            currentZoom: 14,
            currentCenter: [52.375103, 4.890201],
            options: {
                zoomSnap: 0.5,
                maxZoom: 19,
                minZoom: 1
            }
        };
    },
    methods: {
        onReady() {
            this?.$refs?.map?.leafletObject?.locate({
                maximumAge: 86400,
                enableHighAccuracy: true,
                setView: true
            });
        },
        onLocationFound(location) {
            this.location = location;
        }
    }
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
