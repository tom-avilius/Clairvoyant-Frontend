<template>
  <v-form @submit.prevent>
    <v-text-field
      class="spacing"
      :rules="[rule]"
      v-model="query"
      label="Your query"
      variant="outlined"
    ></v-text-field>
    <v-autocomplete
      :rules="[selectedErrorRule]"
      v-model="selectedError"
      label="Select the error type."
      :items="errors"
      variant="outlined"
    ></v-autocomplete>
    <v-textarea
      :rules="[errorDescriptionRule]"
      v-model="errorDescription"
      v-if="showTextArea"
      label="Tell us what happened."
      variant="outlined"
    ></v-textarea>
    <v-btn :loading="loading" class="mt-2" type="submit" @click="load" block
      >Submit</v-btn
    >
  </v-form>

  <v-snackbar-queue
    v-model="errorMsg"
    color="error"
    timeout="2000"
    close-on-content-click="true"
  ></v-snackbar-queue>
</template>

<script setup>
import { ref, watch } from "vue";

const errors = [
  "Fake claim labelled as true.",
  "True claim labelled as false.",
  "Internal/Server Error",
  "Something Else",
];

const loading = ref(false);
const selectedError = ref(null);
const showTextArea = ref(false);
const query = ref("");
const errorMsg = ref([]);
const errorDescription = ref("");

const rule = (v) => {
  const wordCount = v.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount === 0) return "Query cannot be empty.";
  if (wordCount < 4) return "Query must contain at least 4 words.";
  if (wordCount > 100) return "Query must be below 100 words.";
  return true;
};

const selectedErrorRule = (v) => {
  if (v === null) return "Error type cannot be empty.";
  return true;
};

const errorDescriptionRule = (v) => {
  if (v.trim().length < 20) return "Please enter atleast 20 characters.";
  return true;
};

async function load() {
  loading.value = true;

  const wordCount = query.value.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount == 0) {
    errorMsg.value.push("Query cannot be empty.");
  } else if (wordCount < 4) {
    errorMsg.value.push("Query must contain atleast 4 words.");
  } else if (wordCount > 100) {
    errorMsg.value.push("Query must be below 100 words.");
  }

  if (selectedError.value == null) {
    errorMsg.value.push("Error type cannot be empty.");
  }

  if (errorDescription.value.trim().length < 20) {
    errorMsg.value.push(
      "Error description must contain atleast 20 characters.",
    );
  }

  await new Promise((resolve) => setTimeout(resolve, 200));
  loading.value = false;
}

watch(selectedError, (newError, oldError) => {
  if (newError == errors[2] || newError == errors[3]) {
    showTextArea.value = true;
  } else {
    showTextArea.value = false;
  }
});
</script>

<style scoped>
.spacing {
  margin-bottom: 15px;
}
</style>
