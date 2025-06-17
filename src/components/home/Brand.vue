<template>
  <v-container>
    <v-row justify="center" align="baseline">
      <h2 class="text-h2 inline textspacing brand">Clairvoyant:</h2>
      <h4 class="text-h4 inline subtitle">Verify facts and news on the go.</h4>
    </v-row>
  </v-container>
</template>

<style scoped>
.inline {
  display: inline;
}
.textspacing {
  letter-spacing: 4px !important;
}
.brand {
  font-size: 5rem !important;
  font-weight: 400;
  padding-right: 5px;
}
.subtitle {
  font-size: 2.8rem !important;
  font-weight: 300;
  letter-spacing: 1px;
}

@media (max-width: 710px) {
  .brand {
    font-size: 3rem !important;
  }
  .subtitle {
    font-size: 1.8rem !important;
  }
}

@media (max-width: 500px) {
  .brand {
    font-size: 2.5rem !important;
  }
  .subtitle {
    font-size: 1.5rem !important;
  }
}
</style>
