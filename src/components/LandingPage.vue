<template>
  <v-container>
    <v-col lg="8" offset-lg="2">
      <v-stepper v-model="e1">
        <v-stepper-header>
          <v-stepper-step
              :complete="e1 > 1"
              step="1"
              color="teal"
          >
            Choose destination
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step
              :complete="e1 > 2"
              step="2"
          >
            Choose flight
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step step="3">
            Final information
          </v-stepper-step>
        </v-stepper-header>

        <v-stepper-items>

          <v-stepper-content step="1">
            <v-form ref="destinationForm">
              <v-autocomplete
                  class="mt-2"
                  :items="destionations"
                  outlined
                  rounded
                  dense
                  label="Destination"
                  :rules="destinationRules"
              />

              <v-col>
                <v-text-field
                    :value="dates[0]"
                    label="start"
                    outlined
                    rounded
                    dense
                    readonly
                    @click="dateDialog = true"
                    :rules="dateStartRules">
                </v-text-field>
              </v-col>

              <v-col>
                <v-text-field
                    :value="dates[1]"
                    label="end"
                    outlined
                    rounded
                    dense
                    readonly
                    @click="dateDialog = true"
                    :rules="dateEndRules">
                </v-text-field>
              </v-col>

              <v-btn block color="teal" rounded @click="search">
                Search flights
              </v-btn>
            </v-form>
            <v-dialog v-model="dateDialog" width="500px">
              <v-card color="teal">
                <div class="d-flex flex-column">
                  <v-date-picker
                      v-model="dates"
                      color="teal"
                      range>
                  </v-date-picker>
                  <v-btn @click="dateDialog = false" color="teal">Submit</v-btn>
                </div>
              </v-card>
            </v-dialog>
          </v-stepper-content>

          <v-stepper-content step="2">
            <v-row>
              <v-col>
                <v-btn rounded dense outlined block @click="e1 = 1">Cancel</v-btn>
              </v-col>

              <v-col>
                <v-btn rounded dense color="teal" block disabled>Search</v-btn>
              </v-col>
            </v-row>
          </v-stepper-content>

          <v-stepper-content step="3">
            <v-card
                class="mb-12"
                color="grey lighten-1"
                height="200px"
            ></v-card>

            <v-btn
                color="primary"
                @click="e1 = 1"
            >
              Continue
            </v-btn>

            <v-btn text>
              Cancel
            </v-btn>
          </v-stepper-content>
        </v-stepper-items>

      </v-stepper>
    </v-col>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      e1: 1,
      dates: [],
      dateDialog: false,
      destionations: ['Mars', 'Moon'],
      destination: null,
      destinationRules: [v => !!v || 'Destination is required'],
      dateStartRules: [v => !!v || 'Start date is required'],
      dateEndRules: [v => !!v || 'End date is required'],
    }
  },

  methods: {
    search () {
      const isValid = this.$refs["destinationForm"].validate()
      if (!isValid) {
        return
      } else {
        this.e1 = 2
      }
    }
  }
}
</script>

<style scoped>

</style>