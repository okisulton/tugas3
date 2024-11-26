<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Cryptocurrency Prices</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="content">
      <div class="container">
        <ion-button shape="round" @click="fetchData">Refresh</ion-button>
        <CryptoList :cryptos="cryptos" />
        <!-- Tambahkan spacer untuk ruang ekstra -->
        <div class="spacer"></div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import CryptoList from '@/components/CryptoList.vue';
import axios from 'axios';

export default {
  name: 'Home',
  components: { CryptoList },
  data() {
    return {
      cryptos: [],
    };
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://api.coinlore.net/api/tickers/');
        this.cryptos = response.data.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style>
/* Container utama */
.container {
  padding: 0;
  margin: 0 auto;
  text-align: center;
  max-width: 100%;
}

.content {
  height: calc(100vh - var(--ion-safe-area-top) - var(--ion-safe-area-bottom));
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}

.spacer {
  height: 50px;
}
</style>
