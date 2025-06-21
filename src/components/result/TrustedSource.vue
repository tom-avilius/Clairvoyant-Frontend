<template>
  <v-skeleton-loader
    class="no-background"
    v-if="loading"
    :elevation="0"
    type="article"
  />
  <div class="padding" v-else>
    <h4 v-if="data.trusted" class="text-h5 heading">Found a trusted source:</h4>
    <h4 v-else class="text-h5 heading">Found a source:</h4>
    <h6 v-if="data" class="text-subtitle-1 subtitle">{{ data.source }}</h6>
    <p v-if="data" class="text-body-1 text">{{ data.headline }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const loading = ref(true);
const data = ref(null);

// Utility function for delay
const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

onMounted(async () => {
  const uuid = sessionStorage.getItem("uuid");
  if (!uuid) {
    console.error("UUID not found in sessionStorage");
    loading.value = false;
    return;
  }

  try {
    const fetchPromise = fetch(
      "http://localhost:8001/sources?uuid=" + uuid,
    ).then((res) => res.json());

    // Wait for both fetch and delay to finish
    const [fetchedData] = await Promise.all([fetchPromise, delay(1000)]);

    data.value = fetchedData;
  } catch (error) {
    console.error("Error fetching data:", error);
  } finally {
    loading.value = false;
  }
});
</script>

<style scoped>
.no-background {
  background: none !important;
}

.padding {
  margin-left: 15px;
}

.subtitle {
  margin-left: 10px;
  font-weight: 400;
  letter-spacing: 1px !important;
  font-size: 1.1rem !important;
}

.text {
  margin-left: 10px;
  font-size: 1rem !important;
  font-weight: 300 !important;
}

.heading {
  font-size: 1.8rem !important;
  font-weight: 300;
}
</style>
