<template>
  <v-skeleton-loader
    class="no-background"
    v-if="loading"
    :elevation="0"
    type="article"
  />
  <div v-else>
    <h4>Found a trusted source:</h4>
    <h6>{{ data.source }}</h6>
    <p>{{ data.headline }}</p>
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
    const [fetchedData] = await Promise.all([
      fetchPromise,
      delay(2000), // at least 1 second
    ]);

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
</style>
