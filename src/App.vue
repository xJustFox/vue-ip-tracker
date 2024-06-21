<script>
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import {store} from './store.js';
import axios from 'axios';

export default {
  components: {
    AppHeader,
    AppMain,
  },
  data() {
    return {
      store,
      objIp: {},
    }
  },
  methods: {
    getSearch(){
      let apiURL = `${import.meta.env.VITE_API_URL}?apiKey=${import.meta.env.VITE_API_KEY}&ipAddress=${store.searchText}`;

      axios.get(apiURL)
      .then((response) => {
        this.objIp = {
          ipAddress: response.data.ip,
          location: `${response.data.location.city}, ${response.data.location.country} ${response.data.location.region} ${response.data.location.postalCode}`,
          timeZone: response.data.location.timezone,
          isp: response.data.isp,

          lat: response.data.location.lat,
          lng: response.data.location.lng,
        }
      })
      .catch(error => {
        console.log(error.response.data.messages);
      })
    }
  },
}
</script>

<template>
  <AppHeader @button_search="getSearch"></AppHeader>
  <AppMain :ipData="this.objIp"></AppMain>
</template>

<style lang="scss">
@use './style/generals.scss' as *;
  
</style>
