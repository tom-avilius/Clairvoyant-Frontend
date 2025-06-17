<template>
  <v-form @submit.prevent>
    <v-text-field
      v-model="query"
      label="Your query"
      variant="outlined"
    ></v-text-field>
    <v-autocomplete
      v-model="selectedError"
      label="Select the error type."
      :items="errors"
      variant="outlined"
    ></v-autocomplete>
    <v-textarea
      v-if="showTextArea"
      label="Tell us what happened."
      variant="outlined"
    ></v-textarea>
    <v-btn class="mt-2" type="submit" block>Submit</v-btn>
  </v-form>
</template>

<script setup>
import { ref, watch } from "vue";

const errors = [
  "Fake claim labelled as true.",
  "True claim labelled as false.",
  "Internal/Server Error",
  "Something Else",
];

const selectedError = ref(null);
const showTextArea = ref(false);
const query = ref("");

watch(selectedError, (newError, oldError) => {
  if (newError == errors[2] || newError == errors[3]) {
    showTextArea.value = true;
  } else {
    showTextArea.value = false;
  }
});
</script>
