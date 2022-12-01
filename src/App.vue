<template>
  <v-app>
    <v-app-bar app color="teal" dark>
      <v-icon size="46px">mdi-rocket-launch</v-icon>
      <div class="text-h4">RocketBook</div>
      <v-spacer></v-spacer>

      <v-btn text @click="dialogVis = true">
        About Me
      </v-btn>
    </v-app-bar>

    <v-main>
      <LandingPage />
      <v-dialog v-model="dialogVis" width="500px">
        <v-card>
          <div>
            Hello. My name is Maxim, I am a novice IT specialist, and this is one of my projects. Here I get acquainted with how Vuetify 2 is arranged.
          </div>
        </v-card>
        <v-btn @click="dialogVis = false" color="teal">cancel</v-btn>
      </v-dialog>
    </v-main>
  </v-app>
</template>

<script>

import LandingPage from "@/components/LandingPage";
export default {
  name: 'App',

  components: {
    LandingPage
  },

  data: () => ({
    dialogVis: false
  }),
};
</script>
