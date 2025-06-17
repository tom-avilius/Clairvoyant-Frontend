<template>
  <v-footer class="flex">
    <div class="text-left inline">
      <v-btn variant="plain" size="small">Clairvoyant</v-btn>
      <v-btn variant="plain" size="small">
        <v-icon icon="mdi-github"></v-icon>
      </v-btn>
    </div>

    <div class="text-center inline">
      <p class="text-caption">
        Copyright <v-icon icon="mdi-copyright" /> {{ date }}
      </p>
    </div>

    <div class="text-right inline">
      <p class="text-caption">GNU GPLv3 License</p>
    </div>
    <!-- </v-row> -->
  </v-footer>
</template>

<style scoped>
.inline {
  display: inline !important;
}
.flex {
  flex: none !important;
  display: flex !important;
  justify-content: space-between;
}
</style>

<script setup>
const date = new Date().getFullYear();
</script>
