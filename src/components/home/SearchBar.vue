<template>
  <v-text-field
    v-model="query"
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
    </v-btn>
  </v-row>

  <v-snackbar-queue
    v-model="errors"
    color="error"
    timeout="1500"
    close-on-content-click="true"
  ></v-snackbar-queue>
</template>

<script setup>
import { ref, watch } from "vue";

const errors = ref([]);
const query = ref("");
const loading = ref(false);

function load() {
  loading.value = true;
  const wordCount = query.value.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount < 4) {
    errors.value.push("Query must contain atleast 4 words.");
  }

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
