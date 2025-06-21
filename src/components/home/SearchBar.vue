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
// the event fired when the submit btn is clicked
const emit = defineEmits(["update:submitBtnClick"]);

import { ref, watch } from "vue";
import { useRouter } from "vue-router";

// router instance to move to a new page
// when the response is recieved from the
// server
const router = useRouter();

// used for the snackbar to display constraints for
// the text field
const errors = ref([]);
// to store the loading state of the submit btn
// to show the loader
const loading = ref(false);
// v-model parameter to store the text-field input
const query = ref("");

// apply constraints to the input text field.
const rule = (v) => {
  // count the number of words in the text field
  // OPTIMIZE: Use vue math calc for better performance
  const wordCount = v.trim().split(/\s+/).filter(Boolean).length;

  if (wordCount === 0) return "Query cannot be empty.";
  if (wordCount < 4) return "Query must contain at least 4 words.";
  if (wordCount > 100) return "Query must be below 100 words.";
  return true;
};

// handles submit btn click
async function load() {
  // set the loader to display
  loading.value = true;

  // get the word count
  // OPTIMIZE: Use vue math calc for better performance
  const wordCount = query.value.trim().split(/\s+/).filter(Boolean).length;

  // display constraints through the snackbar
  if (wordCount == 0) {
    errors.value.push("Query cannot be empty.");
  } else if (wordCount < 4) {
    errors.value.push("Query must contain atleast 4 words.");
  } else if (wordCount > 100) {
    errors.value.push("Query must be below 100 words.");
  } else {
    // if there have been no errors then

    // fire the submit btn click event to update the brand subtitle
    emit("update:submitBtnClick", true);
    // send a request to the server to analyze the claim
    const res = await fetch("http://127.0.0.1:8001/analyze", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({ news: query.value }),
    });

    // recieve the data
    const data = await res.json();
    // the server also sends a uuid to validate future
    // continuing requests
    sessionStorage.setItem("uuid", data.uuid);

    // route to the result page
    router.push({
      path: "/result",
      query: {
        result: JSON.stringify({ score: data.score, query: query.value }),
      },
    });
  }

  // to ensure the loading state of the btn stays on atleast 0.2sec
  await new Promise((resolve) => setTimeout(resolve, 200));
  // disable loading state of the btn
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
