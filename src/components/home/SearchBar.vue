<template>
  <v-text-field
    class="spacing"
    label="Enter Query"
    prepend-inner-icon="mdi-magnify"
    variant="outlined"
  ></v-text-field>
  <v-row class="spacing-btn" justify="center"
    ><v-btn
      :loading="loading"
      append-icon="mdi-chevron-double-right"
      variant="tonal"
      size="large"
      @click="load"
    >
      Submit
    </v-btn></v-row
  >
</template>

<script setup>
import { ref } from "vue";

const loading = ref(false);
function load() {
  loading.value = true;
  setTimeout(() => (loading.value = false), 3000);
}
</script>

<style scoped>
.spacing {
  margin-top: 12vh;
}
.spacing-btn {
  margin-top: 10px;
}
</style>
