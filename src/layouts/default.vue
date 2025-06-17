<template>
  <v-main>
    <AppBar />
    <v-container class="spacing">
      <router-view />
    </v-container>
  </v-main>

  <AppFooter />
</template>

<script lang="ts" setup>
//
</script>

<style scoped>
.spacing {
  margin-top: 50px;
}
</style>
