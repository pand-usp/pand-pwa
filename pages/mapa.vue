<template>
  <v-container>
    

    <v-row class="text-center mt-1 ml-2">
        <div
          v-for="item in availableAccessibility"
          :key="item"
          class="pa-2 my-2 mx-1 secondary rounded-circle d-inline-block"
        >
          <v-icon color="white" v-if="item === 'fisica'"
            >mdi-barley</v-icon
          >
          <v-icon color="white" v-if="item === 'visual'">mdi-peanut</v-icon>
          <v-icon color="white" v-if="item === 'auditiva'"
            >mdi-bottle-wine</v-icon
          >
        </div>
    </v-row>

    <v-card :loading="loading" class="mt-5">
      <template slot="progress">
        <v-progress-linear
          color="primary"
          height="10"
          indeterminate
        ></v-progress-linear>
      </template>

      <iframe
        width="100%"
        height="250"
        style="border: 0"
        loading="lazy"
        allowfullscreen
        :src="`https://www.google.com/maps/embed/v1/place?key=AIzaSyBOpg8qC16YISD7F7aqj4Xzso3b_JoDX3s&q=${encode()}`"
      >
      </iframe>

      <v-card-title class="pb-0">{{ name }}</v-card-title>

      <v-card-actions>
        <v-btn color="secundary" text @click="goMaps"> Rotas </v-btn>
      </v-card-actions>
    </v-card>

  </v-container>
</template>

<script>
export default {
  asyncData({ query }) {
    return {
      address: query.address,
      name: query.name,
    };
  },
  data() {
    return {
      availableAccessibility: ["fisica", "visual", "auditiva"],
    };
  },
  methods: {
    getApiKey() {
      return process.env.apiKey;
    },
    encode() {
      console.log(this);
      return this.address;
    },
    goMaps() {
      window.location.href = `https://www.google.com.br/maps/search/${this.address}`;
    }

  },
};
</script>
