<template>
  <v-container class="pa-4" flat height="500px">
    <v-row class="my-4">
      <v-col cols="12" align="center">
        <img class="align-center" height="250" src="@/assets/logo_pand.png"/>
      </v-col>
    </v-row>

    <CommonSearch @search="goToLocais" path="locais"/>
    
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
    goToLocais({content, filters}) {
      this.$router.push({ 
        path: `locais/`,
        query: {
          q: content,
          filters: filters.join(','),
        }
      });
    },
    switchColorMode(){
      this.$vuetify.theme.dark = !(this.$vuetify.theme.dark)
    }
  }
}
</script>

<style scoped>
</style>
