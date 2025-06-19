<template>
  <Brand v-model:submitBtnClick="submitBtnClick" />
  <SearchBar v-model:submitBtnClick="submitBtnClick" />
  <Stepper />
</template>

<script setup>
import { ref } from "vue";
const submitBtnClick = ref(false);
</script>
