<template>
  <v-card class="card">
    <h3 class="text-h4 spacing">About Clairvoyant</h3>
    <p class="text-body break">
      Clairvoyant uses a hybrid natural language inference (NLI) pipeline
      designed to analyze and verify claims. It uses advanced language models to
      determine whether a claim is true, false, or uncertain.
    </p>
    <v-divider class="break" />
    <h3 class="text-h4 spacing">The Pipeline</h3>
    <div class="list" v-for="pipe in pipeline" :key="pipe.title">
      <h5 class="text-h6 spacing">{{ pipe.heading }}</h5>
      <p class="text-body-2">{{ pipe.body }}</p>
    </div>
    <p class="break" />
    <v-divider class="break" />
    <h3 class="text-h4 spacing">Result</h3>
    <p class="text-body break">
      A final credibility score is returned (positive = likely true, negative =
      likely false).
    </p>
    <v-divider class="break" />
    <h3 class="text-h4 spacing">License</h3>
    <p class="text-body break">
      Clairvoyant is open-source under the GNU GPLv3 License.
    </p>
  </v-card>
</template>

<script setup>
const pipeline = [
  {
    heading: "Input",
    body: "The user enters a claim through the clairvoyant-frontend, marking the start of the pipeline.",
  },
  {
    heading: "Orchestrator",
    body: "The clairvoyant-orchestrator or simply the Orchestrator orchestrates all the events in the pipeline.",
  },
  {
    heading: "Scraper",
    body: "The Orchestrator gives control to the clairvoyant-scraper that scrapes the web for similar references.",
  },
  {
    heading: "Classifier Model",
    body: "The Classifier classifies the entire data as an entailment, contradiction or neutral.",
  },
  {
    heading: "Sentiment Analysis",
    body: "Sentiment analysis is performed on the provided data to bridge the limitations of the classifier model.",
  },
  {
    heading: "Semantic Analysis",
    body: "To minimize any bias that sentiment analysis may produce, semantic analysis is performed. In the test and reserch a gray area has been found, mostly free from bias, that may be helpful in the future when analyzing large datasets.",
  },
];
</script>

<style scoped>
.card {
  padding: 25px 45px;
  margin-bottom: 20px;
}
.heading {
  padding-bottom: 5px;
}
.spacing {
  padding-top: 10px;
}
.break {
  padding-bottom: 40px;
}
.list {
  padding-top: 15px;
  padding-left: 10px;
}
</style>
