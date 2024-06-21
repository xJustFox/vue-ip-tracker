<script>
import L, { Handler } from 'leaflet';
import 'leaflet/dist/leaflet.css';

export default {
    name: "AppMain",
    data() {
        return {

        }
    },
    watch: {
        'ipData'(value) {

            this.getPositionMap(value.lng, value.lat);
        }
    },
    mounted() {
        // Inizializzazione della mappa
        this.map = L.map('map').setView([
            41.90464, 12.49176], 13);

        // Aggiungere un layer di base
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
        }).addTo(this.map);
    },
    props: {
        ipData: Object,
    },
    methods: {
        getPositionMap(lng, lat) {
            // Inizializzazione della mappa
            this.map.setView([lat, lng], 13);

            // Aggiungere un marker
            L.marker([lat, lng]).addTo(this.map)
                .openPopup();

        }
    },
}
</script>

<template>
    <main>
        <div class="box-capsules">
            <div class="capsul">
                <div class="capsul-title">IP ADDRESS</div>
                <div class="capsul-text">{{ ipData.ipAddress ? ipData.ipAddress : "..." }}</div>
            </div>
            <div class="capsul">
                <div class="capsul-title">LOCATION</div>
                <div class="capsul-text">{{ ipData.location ? ipData.location : "..." }}</div>
            </div>
            <div class="capsul">
                <div class="capsul-title">TIMEZONE</div>
                <div class="capsul-text">{{ ipData.timeZone ? ipData.timeZone : "..." }}</div>
            </div>
            <div class="capsul">
                <div class="capsul-title">ISP</div>
                <div class="capsul-text">{{ ipData.isp ? ipData.isp : "..." }}</div>
            </div>
        </div>

        <div id="map" style="width: 100%; height: 100%; z-index: 0;"></div>

    </main>
</template>

<style lang="scss" scoped>
main {
    @apply relative bg-blue-950 h-svh;

    .box-capsules {
        @apply z-50 absolute top-[-150px] lg:top-[-50px] left-2/4 -translate-x-2/4 flex flex-col lg:flex-row bg-slate-50 rounded-lg;

        .capsul {
            @apply p-3 lg:p-5 border-black;

            .capsul-title {
                @apply text-slate-600
            }

            .capsul-text {
                @apply w-[300px] lg:w-[200px] 2xl:w-[300px] font-semibold text-lg;
            }
        }
    }
}

@media screen and (min-width: 1024px) {
    main {
        height: calc(100vh - 200px);
    }
}
</style>