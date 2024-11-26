<template>
    <ion-list class="crypto-list">
      <CryptoItem v-for="crypto in cryptos" :key="crypto.id" :crypto="crypto" />
    </ion-list>
  </template>
  
  <script>
  import CryptoItem from './CryptoItem.vue';
  
  export default {
    name: 'CryptoList',
    components: { CryptoItem },
    props: {
      cryptos: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .crypto-list {
    padding: 0;
    margin: 0;
    width: 100%;
  }
  </style>
  