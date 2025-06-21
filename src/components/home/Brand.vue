<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="auto">
        <div class="title-grid">
          <h2 class="brand">Clairvoyant:</h2>
          <transition name="fade-slide" mode="out-in">
            <h4 :key="msg" class="subtitle">
              {{ msg }}
            </h4>
          </transition>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, watch } from "vue";

// to change the brand subtitle when the submit btn is clicked or
// the enter key is pressed
const props = defineProps(["submitBtnClick"]);

// to store the brand subtitle and change it reactively
const msg = ref("Verify facts and news on the go.");

// listen to the event when the submit btn is clicked
watch(
  () => props.submitBtnClick,
  (newVal) => {
    if (newVal) {
      // update the value accordingly
      msg.value = "Sending data to our servers..";
      // introduce delay when upgrading further
      setTimeout(() => {
        msg.value = "We are working on it..";
      }, 2000);
      setTimeout(() => {
        msg.value = "Fetching References..";
      }, 4000);
      setTimeout(() => {
        msg.value = "Processing..";
      }, 6000);
      setTimeout(() => {
        msg.value = "Running our NLI pipeline..";
      }, 8000);
      setTimeout(() => {
        msg.value = "Performing text classification..";
      }, 10000);
      setTimeout(() => {
        msg.value = "Analyzing sentiment..";
      }, 12000);
      setTimeout(() => {
        msg.value = "Checking semantics..";
      }, 14000);
      setTimeout(() => {
        msg.value = "This is taking longer than usual..";
      }, 16000);
    }
  },
);
</script>

<style scoped>
.title-grid {
  width: 100vw;
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: baseline;
  column-gap: 0.75rem;
}

/* Animation */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.3s ease;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(10px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

/* Typography */
.brand {
  font-size: 5rem;
  font-weight: 400;
  letter-spacing: 4px;
}
.subtitle {
  font-size: 2.8rem;
  font-weight: 300;
  letter-spacing: 1px;
}

/* Responsive */
@media (max-width: 1280px) {
  .brand,
  .subtitle {
    justify-self: start;
  }
  .brand {
    font-size: 4rem;
  }
  .subtitle {
    font-size: 2rem;
  }
}
@media (max-width: 900px) {
  .title-grid {
    grid-template-columns: 1fr;
    row-gap: 0.5rem;
  }
  .brand,
  .subtitle {
    justify-self: start;
  }
  .brand {
    font-size: 4rem;
  }
  .subtitle {
    font-size: 2.2rem;
  }
}

@media (max-width: 710px) {
  .title-grid {
    grid-template-columns: 1fr;
    row-gap: 0.5rem;
  }
  .brand,
  .subtitle {
    justify-self: start;
  }
  .brand {
    font-size: 3rem;
  }
  .subtitle {
    font-size: 1.8rem;
  }
}

@media (max-width: 500px) {
  .title-grid {
    grid-template-columns: 1fr;
    row-gap: 0.5rem;
  }
  .brand,
  .subtitle {
    justify-self: start;
  }
  .brand {
    font-size: 2.5rem;
  }
  .subtitle {
    font-size: 1.5rem;
  }
}
</style>
