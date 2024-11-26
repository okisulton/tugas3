<template>
    <ion-item lines="none" class="crypto-item">
      <div class="crypto-container">
        <!-- Kolom Rank -->
        <div class="crypto-rank">
          <div>Rank</div>
          <div><h3>{{ crypto.rank }}</h3></div>
        </div>
  
        <!-- Kolom Name dan Symbol -->
        <div class="crypto-name">
          <div>{{ crypto.name }}</div>
          <div><h3>{{ crypto.symbol }}</h3></div>
        </div>
  
        <!-- Kolom Price USD -->
        <div class="crypto-price">
          <div>USD</div>
          <div><h3>{{ crypto.price_usd }}</h3></div>
        </div>
      </div>
    </ion-item>
  </template>
  
  <script>
  export default {
    name: 'CryptoItem',
    props: {
      crypto: {
        type: Object,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .crypto-item {
    padding: 0;
    margin: 0;
    width: 100%;
  }
  
  .crypto-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #fff3cd;
    border: 1px solid #f0c36d;
    padding: 8px 16px;
    width: 100%;
    box-sizing: border-box;
  }
  
  .crypto-rank {
    text-align: left;
  }
  
  .crypto-name {
    text-align: center;
  }
  
  .crypto-price {
    text-align: right;
  }
  </style>
  