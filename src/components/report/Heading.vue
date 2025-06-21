<template>
  <v-container class="margin">
    <h4 class="text-h4 subtitle">
      Did you notice any inconsistency in the result?
    </h4>
    <h6 class="caption">Help us by reporting errors!</h6>
    <p class="text-body-1 text">How would rate us:</p>
    <v-rating
      hover
      :length="5"
      :size="30"
      :model-value="3"
      active-color="primary"
    />
  </v-container>
</template>

<style scoped>
.text {
  margin-top: 20px;
  font-size: 1rem !important;
  font-weight: 300 !important;
}

.subtitle {
  font-size: 2.8rem !important;
  font-weight: 300;
  letter-spacing: 2px;
}

.margin {
  margin-bottom: 40px;
}

.caption {
  font-size: 1.5rem;
  font-weight: 300 !important;
  letter-spacing: 1px;
}

@media (max-width: 710px) {
  .caption {
    font-size: 1.2rem;
  }
  .subtitle {
    font-size: 1.8rem !important;
  }
}

@media (max-width: 500px) {
  .caption {
    font-size: 1rem;
  }
  .subtitle {
    font-size: 1.5rem !important;
  }
}
</style>
