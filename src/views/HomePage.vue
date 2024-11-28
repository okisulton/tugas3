<template>
  <ion-page>
    <CryptoTable />
  </ion-page>
</template>

<script>
import { IonPage } from '@ionic/vue';
import CryptoTable from '../components/CryptoTable.vue';

export default {
  components: {
    IonPage,
    CryptoTable
  }
};
</script>