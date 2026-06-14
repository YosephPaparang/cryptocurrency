<template>
  <ion-page>
    <ion-content class="ion-padding">
      <div class="refresh-container">
        <button class="btn-refresh" @click="fetchCryptoData">Refresh</button>
      </div>

      <div v-if="isLoading" class="loading-container">
        <ion-spinner name="crescent"></ion-spinner>
      </div>

      <div v-else class="crypto-list">
        <div v-for="coin in cryptoList" :key="coin.id" class="crypto-item">
          <div class="col-rank">
            <span class="label">Rank</span>
            <span class="value-large">{{ coin.rank }}</span>
          </div>

          <div class="col-name">
            <span class="label">{{ coin.name }}</span>
            <span class="value-large">{{ coin.symbol }}</span>
          </div>

          <div class="col-price">
            <span class="label">USD</span>
            <span class="value-large">{{ formatPrice(coin.price_usd) }}</span>
          </div>
        </div>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { IonPage, IonContent, IonSpinner } from '@ionic/vue';

const cryptoList = ref<any[]>([]);
const isLoading = ref<boolean>(false);

const fetchCryptoData = async () => {
  isLoading.value = true;
  try {
    const response = await fetch('https://api.coinlore.net/api/tickers/');
    if (!response.ok) throw new Error('Gagal mengambil data');
    const result = await response.json();
    cryptoList.value = result.data;
  } catch (error) {
    console.error('Error fetching data:', error);
  } finally {
    isLoading.value = false;
  }
};

const formatPrice = (price: string) => {
  const num = parseFloat(price);
  return num > 1 ? num.toFixed(2) : num.toFixed(6);
};

onMounted(() => {
  fetchCryptoData();
});
</script>

<style scoped>
.refresh-container {
  display: flex;
  justify-content: center;
  margin-bottom: 16px;
}

.btn-refresh {
  background-color: #0062e1;
  color: white;
  border: none;
  padding: 10px 40px;
  font-size: 16px;
  border-radius: 4px;
  cursor: pointer;
}

.btn-refresh:active {
  background-color: #004db2;
}

/* Loading style */
.loading-container {
  display: flex;
  justify-content: center;
  margin-top: 50px;
}

.crypto-list {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.crypto-item {
  background-color: #fef4cd;
  border: 1px solid #e6d7a7;
  padding: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.col-rank {
  width: 15%;
  display: flex;
  flex-direction: column;
}

.col-name {
  width: 45%;
  display: flex;
  flex-direction: column;
}

.col-price {
  width: 40%;
  display: flex;
  flex-direction: column;
}

.label {
  font-size: 11px;
  color: #555;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.value-large {
  font-size: 22px;
  color: #000;
  font-weight: 400;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>