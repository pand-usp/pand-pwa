<template>
  <v-container>
    <v-row align="center" justify="space-around" class="pt-8">
      <v-col cols="12" sm="8" md="6" align-items="center">
        <v-card-text class="title font-weight-bold pt-0"
          ><h1>{{ name }}</h1></v-card-text
        >
        <v-card-subtitle
          ><h3>{{ address }}</h3></v-card-subtitle
        >
        <v-img
          class="rounded-xl"
          elevation="0"
          :aspect-ratio="16/9"
          height="20%"
          :src="image"
        ></v-img>
        <v-card-actions
          class="d-flex flex-column"
          align-items="center"
          width="auto"
        >
          <v-btn
            class="text-center white--text rounded-xl"
            color="secondary"
            elevation="2"
            width="240"
            nuxt
            large
            :to="`/mapa?address=${address}`"
          >
            <h4>Confira as Atrações!</h4>
          </v-btn>
        </v-card-actions>

        <v-card-title
          ><span class="secondary--text p-0"
            ><h3>Avaliações e Comentários</h3></span
          ></v-card-title
        >

        <v-row no-gutters class="mb-5">
          <v-col cols="6">
            <div class="d-flex flex-column align-center justify-center">
              <h1> {{ getRatingAvg() }}</h1>
              <v-rating
                color="primary"
                hover
                length="5"
                readonly
                dense
                size="18"
                :value="getRatingAvg()"
              ></v-rating>
            </div>
          </v-col>
          <v-col cols="6">
            <div class="d-flex my-2"
              v-if="accessibility.includes('fisica')"
            >
              <v-icon color="secondary">mdi-wheelchair-accessibility</v-icon>
              <v-rating
                color="primary"
                hover
                length="5"
                readonly
                dense
                size="25"
                :value="rating.fisica"
              ></v-rating>
            </div>
            <div class="d-flex my-2"
              v-if="accessibility.includes('visual')"
            >
              <v-icon color="secondary">mdi-eye-off</v-icon>
              <v-rating
                color="primary"
                hover
                length="5"
                readonly
                dense
                size="25"
                :value="rating.visual"
              ></v-rating>
            </div>
            <div class="d-flex my-2" 
              v-if="accessibility.includes('auditiva')"
            >
              <v-icon color="secondary">mdi-ear-hearing-off</v-icon>
              <v-rating
                color="primary"
                hover
                length="5"
                readonly
                dense
                size="25"
                :value="rating.auditiva"
              ></v-rating>
            </div>
          </v-col>
        </v-row>


        <div v-for="comment in comments" :key="comment.text">
          <v-card elevation="3" color="blocos">
            <v-card-subtitle
              ><span class="secondary--text">
                <h2>{{ comment.author }}</h2>
              </span></v-card-subtitle
            >
            <v-card-text>{{
              "Deficiência " +
              Object.keys(comment.condition).filter(
                (key) => comment.condition[key] === true
              )[0]
            }}</v-card-text>
            <v-card-text>{{ comment.text }}</v-card-text> </v-card
          ><br />
        </div>
      </v-col>
    </v-row>

    <v-card-title
      ><span class="secondary--text"><h2>Comunidades</h2></span></v-card-title
    >
    <v-card-subtitle
      ><h4>
        Este lugar foi muito citado nas seguintes comunidades:
      </h4></v-card-subtitle
    >
    
    <ComunidadeCard 
      v-for="community in communities"
      :key="community.id"
      :name="community.name"
      :description="community.description"
    />
  </v-container>
</template>

<script>
export default {
  async asyncData({ params, query, $axios }) {
    const data = await $axios.$get(`/place/${params.id}`);
    const communities = await $axios.$get(`/community`);
    return {
      ...data,
      address: query.address,
      name: query.name,
      accessibility: query.accessibility.split(","),
      image: query.image,
      communities: communities
    };
  },
  methods: {
    goToMapa() {
      console.log(this.address);
      this.$router.push({
        path: "/mapa",
        params: {
          q: encodeURI(this.address),
          name: this.name
        },
      });
    },
    getRatingAvg() {
      let count = 0;
      if (this.rating.visual) {
        count++;
      }
      if (this.rating.auditiva) {
        count++;
      }
      if (this.rating.fisica) {
        count++;
      }
      return ((this.rating.visual + this.rating.auditiva + this.rating.fisica)/count).toFixed(2);
    },
    goToComunidade() {
      this.$router.push('/grupo')
    }
  },
};
</script>
        