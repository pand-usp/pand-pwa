<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6" align-items="center">
        <v-card light class="py-4 d-flex flex-column" align="center">
          <v-card-title class="headline justify-center">
            <h2>Adicione o Local</h2>
          </v-card-title>
          
          <v-card-actions class="d-flex flex-column" align-items="center" width="auto">
            <v-row>
              <br/>
                <v-text-field
                  v-model="name"
                  label="Nome"
                  required
                ></v-text-field>
            </v-row>

            <br/>
              <v-row>
              <v-text-field
                v-model="address"
                label="Endereço"
                append-icon="mdi-map-marker"
                required
              ></v-text-field>
                </v-row>

            <br/>
            <v-row>
              <v-text-field
                v-model="image"
                append-icon="mdi-camera"
                label="Imagem"
                required
              ></v-text-field>
            </v-row>
          
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-barley</v-icon>
              <v-rating
                align="center"
                v-model="ratingFisica"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-peanut</v-icon>
              <v-rating
                align="center"
                v-model="ratingVisual"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-bottle-wine</v-icon>
              <v-rating
                align="center"
                v-model="ratingAuditiva"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
            
            <v-card-actions class="d-flex flex-column" align-items="center" width="auto">
              <v-btn
                  class="text-xs-center black--text" 
                  color="primary"
                  elevation="2"
                  @click="addLocal"
              >
                  Cadastrar local
              </v-btn>
            </v-card-actions>

          </v-card-actions>
        </v-card>

      </v-col>
    </v-row>
  </v-container>
</template>


<script>

export default {
  data() {
    return {
      locais: [],
      name: "",
      address: "",
      image: "",
      ratingFisica: 0,
      ratingVisual: 0,
      ratingAuditiva: 0,
    }
  },
  
  methods: {
    async addLocal () {
      await setTimeout(() => {}, 100)
      const response = await this.$axios.$post('/place', {
        name: this.$data.name,
        address: this.$data.address,
        imageURL: this.$data.image,
        rating: { 
            auditiva : this.$data.ratingAuditiva, 
            fisica : this.$data.ratingFisica, 
            visual : this.$data.ratingVisual, 
          },
        accessibility : { 
            auditiva : this.$data.ratingAuditiva > 0 ? true : false, 
            fisica : this.$data.ratingFisica > 0 ? true : false,
            visual : this.$data.ratingVisual > 0 ? true : false,
          }
      });

      console.log(this.$data.ratingAuditiva)

      this.$router.push({ 
        path: `locais/`,
      });

    },
  },
}
</script>

