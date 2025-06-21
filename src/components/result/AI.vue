<template>
  <v-container class="padding">
    <h4 class="text-h5 heading">What AI has to say:</h4>
    <v-skeleton-loader
      v-if="!text"
      class="no-background"
      type="paragraph"
    ></v-skeleton-loader>
    <p v-else class="text text-body-1">{{ text }}</p>
  </v-container>
</template>

<style scoped>
.no-background {
  background: none !important;
}

.padding {
  margin-top: 30px;
}

.text {
  margin-left: 10px;
  font-size: 1rem !important;
  font-weight: 300 !important;
}

.heading {
  font-size: 1.8rem !important;
  font-weight: 300;
}
</style>

<script setup>
const apiKey = import.meta.env.VITE_API_KEY;
import { useRoute } from "vue-router";
import { ref } from "vue";

const text = ref(null);

const route = useRoute();
const result = JSON.parse(route.query.result || "{}");

fetch(
  `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${apiKey}`,
  {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      contents: [
        {
          parts: [
            {
              text: result.query,
            },
          ],
        },
      ],
    }),
  },
)
  .then((response) => response.json())
  .then((data) => {
    setTimeout(() => {}, 200);
    text.value = data.candidates?.[0]?.content?.parts?.[0]?.text;
  })
  .catch((error) => {
    console.error("Error:", error);
  });
</script>
