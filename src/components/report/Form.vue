<template>
  <v-form @submit.prevent>
    <v-text-field
      :rules="[rule]"
      class="spacing"
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

// a list of errors that may occur
// for the user to select and report.
// WARN: Not a complete or even tested list.
const errors = [
  "Fake claim labelled as true.",
  "True claim labelled as false.",
  "Internal/Server Error",
  "Something Else",
];

// the loading state of the submit btn
const loading = ref(false);
// the constraints for the selection input element
const selectedError = ref(null);
// flag to display the text area
const showTextArea = ref(false);
// the query entered by the user in the
// home page
const query = ref("");
// to display the contraint errors using the
// snackbar.
const errorMsg = ref([]);
// contraints for the text area input
const errorDescription = ref("");

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


// to evaluate constraints for the selection element
const selectedErrorRule = (v) => {
  if (v === null) return "Error type cannot be empty.";
  return true;
};

// to evaluate contraints for the text area element
const errorDescriptionRule = (v) => {
  if (v.trim().length < 20) return "Please enter atleast 20 characters.";
  return true;
};

// handle submit btn click
async function load() {
  // set the loading state
  loading.value = true;

  // display selection input error if any
  if (selectedError.value == null) {
    errorMsg.value.push("Error type cannot be empty.");
  }

  // display text area errors if any
  if (errorDescription.value.trim().length < 20) {
    errorMsg.value.push(
      "Error description must contain atleast 20 characters.",
    );
  }

  // get the word count
  // OPTIMIZE: Use vue math calc for better performance
  const wordCount = query.value.trim().split(/\s+/).filter(Boolean).length;

  // display constraints through the snackbar
  if (wordCount == 0) {
    errorMsg.value.push("Query cannot be empty.");
  } else if (wordCount < 4) {
    errorMsg.value.push("Query must contain atleast 4 words.");
  } else if (wordCount > 100) {
    errorMsg.value.push("Query must be below 100 words.");
  }

  // ensure the loading state is atleast 0.2s
  await new Promise((resolve) => setTimeout(resolve, 200));
  // disable the loading state
  loading.value = false;
}


// to control when to display the text area
watch(selectedError, (newError) => {

  // only display text area for bottom two errors
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
