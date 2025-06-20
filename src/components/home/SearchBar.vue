<template>
  <v-text-field
    @keyup.enter="load"
    :rules="[rule]"
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
    timeout="2000"
    close-on-content-click="true"
  ></v-snackbar-queue>
</template>

<script setup>
const emit = defineEmits(["update:submitBtnClick"]);
import { ref, watch } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const errors = ref([]);
const loading = ref(false);
const query = ref("");

const rule = (v) => {
  const wordCount = v.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount === 0) return "Query cannot be empty.";
  if (wordCount < 4) return "Query must contain at least 4 words.";
  if (wordCount > 100) return "Query must be below 100 words.";
  return true;
};

async function load() {
  loading.value = true;

  const wordCount = query.value.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount == 0) {
    errors.value.push("Query cannot be empty.");
  } else if (wordCount < 4) {
    errors.value.push("Query must contain atleast 4 words.");
  } else if (wordCount > 100) {
    errors.value.push("Query must be below 100 words.");
  } else {
    emit("update:submitBtnClick", true);
    const res = await fetch("http://127.0.0.1:8001/analyze", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ news: query.value }),
    });

    const data = await res.json();
    sessionStorage.setItem("uuid", data.uuid);
    router.push({
      path: "/result",
      query: {
        result: JSON.stringify({ score: data.score, query: query.value }),
      },
    });
  }

  await new Promise((resolve) => setTimeout(resolve, 200));
  loading.value = false;
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
