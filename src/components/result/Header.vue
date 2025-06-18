<template>
  <v-container class="margin">
    <h4 class="text-h4 subtitle">The claim is probably {{ verdict }}.</h4>
    <h6 class="caption">We found {{ report }} evidence.</h6>
  </v-container>
</template>

<style scoped>
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

<script setup>
import { useRoute } from "vue-router";

const route = useRoute();
const result = JSON.parse(route.query.result || "{}");
const verdict = result >= 0 ? "TRUE" : "FALSE";
const report = result >= 0 ? "similar" : "contradicting";
</script>
