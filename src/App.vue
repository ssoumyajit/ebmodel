<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="@/assets/logo.png"
          transition="scale-transition"
          width="100">
        
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="www.ebmtech.com"
        target="_blank"
        text
      >
        <span class="mr-2">About EBM Technologies</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <ModelUploader/>
    </v-main>
  </v-app>
</template>

<script>
import ModelUploader from './components/ModelUploader';

export default {
  name: 'App',

  components: {
    ModelUploader,
  },

  data: () => ({
    //
  }),
};
</script>
