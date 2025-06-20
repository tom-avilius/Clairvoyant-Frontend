<template></template>

<script setup>
const uuid = sessionStorage.getItem("uuid");
const result = await fetch("http://localhost:8001/sources?uuid=" + uuid);
console.log(result.json());
</script>
