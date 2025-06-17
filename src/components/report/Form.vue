<template>
  <v-form @submit.prevent>
    <v-text-field label="Your query" variant="outlined"></v-text-field>
    <v-autocomplete
      label="Select the error type."
      :items="[
        'Fake claim labelled as true.',
        'True claim labelled as false.',
        'Internal/Server Error',
        'Something Else',
      ]"
      variant="outlined"
    ></v-autocomplete>
    <v-textarea label="Tell us what happened." variant="outlined"></v-textarea>
    <v-btn class="mt-2" type="submit" block>Submit</v-btn>
  </v-form>
</template>

<script setup>
import { ref } from "vue";

const firstName = ref("");

const rules = [
  (value) => {
    if (value) return true;
    return "You must enter a first name.";
  },
];
</script>
