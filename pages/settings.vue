<template>
  <v-container>
    <v-row >
      <v-col cols="12" sm="8" md="6">
        <v-card light>
          <v-card-title class="headline justify-center">
            <h2>Configurações</h2>
          </v-card-title>
          <v-card-actions class="d-flex flex-column">
            <v-row class="pt-8">
              Acessibilidde Cores
            </v-row>
            <v-row class="mb-1">
              <v-switch
                @click="switchColorMode"
                v-model="switch1"
                inset
                label="Daltonismo"
              ></v-switch>
            </v-row>
          </v-card-actions>
        </v-card>
          <!-- fazer uma gambiarra p deixar bonito só, ja q n vamos usar -->

      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data() {
    return {
      amenities: []
    }
  },
  methods: {
    switchColorMode(){
      this.$vuetify.theme.dark = !(this.$vuetify.theme.dark)
    }
  }
}
</script>

<style scoped>
</style>
