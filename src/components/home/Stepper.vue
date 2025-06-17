<template>
  <v-stepper class="spacing" editable :items="['Step 1', 'Step 2', 'Step 3']">
    <template v-slot:item.1>
      <v-card title="Step One" flat>
        <p class="text">
          Enter the fact or news you desire to verify in the search bar.
        </p>
      </v-card>
    </template>

    <template v-slot:item.2>
      <v-card title="Step Two" flat>
        <p class="text">Wait for the server to validate your query.</p>
      </v-card>
    </template>

    <template v-slot:item.3>
      <v-card title="Step Three" flat>
        <p class="text">
          Once the validation is complete, the validation window would open to
          show you the results. If the results are not what you expected, please
          <v-btn>report</v-btn> to us.
        </p>
      </v-card>
    </template>
  </v-stepper>
</template>

<style scoped>
.spacing {
  margin-top: 100px;
  background: none !important;
}
.v-card {
  background: none !important;
}
.text {
  padding-left: 16px !important;
}
</style>
