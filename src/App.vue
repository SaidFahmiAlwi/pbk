<script setup>
import { ref, computed, watch, onMounted, onUpdated, onUnmounted } from 'vue';

const items = ref(["buku", "pena", "pensil", "penghapus"]);
const newItem = ref("");

const addItem = () => {
  if (newItem.value.trim() !== "") {
    items.value.push(newItem.value.trim());
    newItem.value = "";
  }
};

// Harga Barang & Pajak
const price = ref(48000);
const tax = ref(3);
const totalPrice = computed(() => price.value + (price.value * (tax.value / 100)));

const formatRupiah = (value) => 'Rp ' + value.toLocaleString('id-ID');

// Status Baterai
const batteryLevel = ref(80);
const status = ref("Normal");

watch(batteryLevel, (newValue, oldValue) => {
  console.log(`Battery level changed: ${oldValue} -> ${newValue}`);
  if (newValue >= 80) {
    status.value = "Baterai Penuh 🟢";
  } else if (newValue >= 30) {
    status.value = "Normal";
  } else {
    status.value = "Baterai Lemah ⚠️";
  }
});

// Lifecycle Hooks
onMounted(() => {
  console.log("✅ Komponen berhasil dimuat! (onMounted)");
});

onUpdated(() => {
  console.log("🔄 Komponen diperbarui! (onUpdated)");
});

onUnmounted(() => {
  console.log("❌ Komponen dihapus dari DOM! (onUnmounted)");
});
</script>

<template>
  <div class="container">
    <ul class="product-list">
      <li v-for="(item, index) in items" :key="index">
        {{ index + 1 }}. {{ item }}
      </li>
    </ul>

    <div class="input-group">
      <input v-model="newItem" type="text" placeholder="Masukkan nama barang" />
      <button @click="addItem">Tambah Barang</button>
    </div>

    <div class="card">
      <h2>Harga dengan Pajak:</h2>
      <label>Harga Barang:</label>
      <input v-model.number="price" type="number" min="0" />

      <label>Pajak (%):</label>
      <input v-model.number="tax" type="number" min="0" />

      <p>Harga Barang: <strong>{{ formatRupiah(price) }}</strong></p>
      <p>Pajak: <strong>{{ tax }}%</strong></p>
      <p>Total Harga: <strong>{{ formatRupiah(totalPrice) }}</strong></p>
    </div>

    <div class="card">
      <h2>Status Baterai</h2>
      <p>Masukkan persentase baterai:</p>
      <input v-model.number="batteryLevel" type="number" min="0" max="100" />
      <p>Status: <strong>{{ status }}</strong></p>
    </div>
  </div>
</template>

<style scoped>
/* Container utama */
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Daftar Barang */
.fruit-list {
  padding: 0;
  margin-bottom: 20px;
  list-style: none;
}

.product-list li {
  background-color: #e0f7fa;
  padding: 10px;
  margin: 5px 0;
  border-radius: 5px;
}

/* Input Group */
.input-group {
  display: flex;
  margin-bottom: 20px;
}

.input-group input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px 0 0 5px;
  outline: none;
}

.input-group button {
  padding: 10px 15px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 0 5px 5px 0;
  cursor: pointer;
}

.input-group button:hover {
  background-color: #0056b3;
}

/* Card styling */
.card {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.card h2 {
  margin-bottom: 15px;
}

.card input {
  width: 100%;
  padding: 8px;
  margin: 8px 0;
  border: 1px solid #ccc;
  border-radius: 5px;
  outline: none;
}

/* Strong text styling */
.card p strong {
  color: #333;
}

/* Responsive design */
@media (max-width: 600px) {
  .container {
    padding: 10px;
  }

  .input-group {
    flex-direction: column;
  }

  .input-group input,
  .input-group button {
    width: 100%;
    margin: 5px 0;
  }
}
</style>
