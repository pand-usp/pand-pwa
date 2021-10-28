<template>
  <v-card class="my-8" elevation="3" color="blocos" @click="goToComunidade">
    <v-row class="text-center mt-1" justify="center">
      <v-col cols="1" md="1"></v-col>
      <v-col cols="2" md="2">
        <v-img class="rounded-circle pa-7" aspect-ratio="1" src="https://images.unsplash.com/photo-1517604931442-7e0c8ed2963c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=750&q=80"></v-img>
      </v-col>
      <v-col cols="9">
        <v-card-subtitle><span class="secondary--text"><h2>{{ name }}</h2></span></v-card-subtitle>        
        <v-card-text>{{ description }}</v-card-text>
      </v-col>
    </v-row>
  </v-card>
</template>

<script>
export default {
  props: ['name', 'description'],
  methods: {
    goToComunidade() {
      this.$router.push('/grupo')
    }
  }
}
</script>