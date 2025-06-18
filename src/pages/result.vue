<template></template>

<script setup>
import { useRoute } from "vue-router";

const route = useRoute();
const result = JSON.parse(route.query.result || "{}");
console.log(result);
</script>
