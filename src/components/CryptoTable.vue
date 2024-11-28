<template>
    <ion-page>
      <ion-header>
        <ion-toolbar>
          <ion-title>Crypto Prices</ion-title>
        </ion-toolbar>
      </ion-header>
  
      <ion-content>
        <div class="container">
          <ion-button @click="fetchData" color="primary">Refresh</ion-button>
  
          <!-- Menampilkan data dengan ion-list dan ion-item -->
          <ion-list v-if="cryptoData.length > 0" class="crypto-list">
            <ion-item v-for="(crypto, index) in cryptoData" :key="crypto.id" lines="full" class="crypto-item">
              <div class="crypto-container">
                <ion-grid>
                    <ion-row>
                    <ion-col size="4" class="item-rank">
                        <p>Rank</p>
                        <span>{{ crypto.rank }}</span>
                    </ion-col>
                    <ion-col size="4" class="item-name">
                        <p>{{ crypto.name }}</p>
                        <span>{{ crypto.symbol }}</span>
                    </ion-col>
                    <ion-col size="4" class="item-usd">
                        <p>USD</p>
                        <span>${{ crypto.price_usd }}</span>
                    </ion-col>
                    </ion-row>
                </ion-grid>
              </div>
                
            </ion-item>
          </ion-list>
  
          <div v-else>
            <p>No data available. Click "Refresh" to fetch cryptocurrency prices.</p>
          </div>
        </div>
      </ion-content>
    </ion-page>
  </template>
  
  <script>
  import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonButton, IonList, IonItem, IonGrid, IonRow, IonCol } from '@ionic/vue';
  import axios from 'axios';
  
  export default {
    name: 'CryptoTable',
    components: {
      IonPage,
      IonHeader,
      IonToolbar,
      IonTitle,
      IonContent,
      IonButton,
      IonList,
      IonItem,
      IonGrid,
      IonRow,
      IonCol,
    },
    data() {
      return {
        cryptoData: [],  // Array untuk menyimpan data kripto
      };
    },
    methods: {
      async fetchData() {
        try {
          const response = await axios.get('https://api.coinlore.net/api/tickers/');
          this.cryptoData = response.data.data.map((crypto) => ({
            id: crypto.id,
            rank: crypto.rank,
            name: crypto.name,
            symbol: crypto.symbol,
            price_usd: crypto.price_usd,
          }));
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
  
<style scoped>
    .container {
        padding: 16px;
        text-align: center;
    }
    
    ion-button {
        margin-bottom: 16px;
    }

    .crypto-list {
        padding: 0;
        margin: 0;
        width: 100%;
    }

    .crypto-item {
        padding: 0;
        margin: 0;
        width: 100%;
        border: 1px solid #6c4f3d; /* coklat tua */
    }

    .crypto-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 8px 16px;
        width: 100%; /* memastikan container mengambil seluruh lebar */
    }

    ion-grid {
        width: 100%; /* memastikan grid mengambil seluruh lebar */
        padding: 0;  /* menghapus padding default agar lebar grid penuh */
        margin: 0;   /* menghapus margin default */
    }

    ion-row {
        display: flex;
        justify-content: space-between; /* memastikan kolom terdistribusi merata */
        width: 100%; /* memastikan row mengambil seluruh lebar */
    }

    ion-col {
        background-color: inherit; /* mewarisi latar belakang dari ion-item */
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 0; /* menghapus padding agar kolom lebih lebar */
        width: 33.33%; /* memastikan setiap kolom memiliki lebar 1/3 dari grid */
    }

    .item-rank, .item-name, .item-usd {
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: inherit; /* mewarisi latar belakang dari parent */
        padding: 8px 0;
    }

    .item-rank p, .item-name p, .item-usd p {
        font-size: 12px;
        color: #000;
        margin: 0;
    }

    .item-rank span, .item-name span, .item-usd span {
        font-size: 16px;
        font-weight: bold;
        color: #000;
    }
</style>
  