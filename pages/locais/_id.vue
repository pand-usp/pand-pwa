<template>
  <v-card class="ma-4" light elevation="0">
    <v-row align="center" justify="space-around" class="pt-8">
      <v-col cols="12" sm="8" md="6" align-items="center">
        <v-card-text light class="title font-weight-bold pt-0 black--text"
          ><h1>{{ name }}</h1></v-card-text
        >
        <v-card-subtitle class="black--text"
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
            class="text-center white--text rounded-xl black--text"
            color="secondary"
            elevation="2"
            width="240"
            nuxt
            large
            :to="`/mapa?address=${address}`"
          >
            <h4>Confira o Mapa!</h4>
          </v-btn>
        </v-card-actions>

        <v-card-title
          ><span class="secondary--text p-0 black--text"
            ><h3>Avaliações e Comentários</h3></span
          ></v-card-title
        >

        <v-row no-gutters class="mb-5">
          <v-col cols="6">
            <div class="d-flex flex-column align-center justify-center black--text">
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

        <v-divider class="mx-4"></v-divider>

        <div class="pb-4">
          <br/>
            <v-card class="pa-2" elevation="0" align="center">
              <v-text-field
                v-model="comment"
                color="secondary"
                align="center"
                label="Deixe seu comentário"
                append-outer-icon="mdi-send"
                required
                @click:append-outer="sendMessage"
              ></v-text-field>
    
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-wheelchair-accessibility</v-icon>
              <v-rating
                align="center"
                v-model="rating2"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-eye-off</v-icon>
              <v-rating
                align="center"
                v-model="rating2"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
            <div class="d-flex my-2">
              <v-icon color="secondary">mdi-ear-hearing-off</v-icon>
              <v-rating
                align="center"
                v-model="rating2"
                background-color="primary"
                color="primary"
                large
              ></v-rating>
            </div>
          </v-card>
        </div>

        <div v-for="comment in comments" :key="comment.text">
          <v-card elevation="3" color="blocos">
            <v-card-subtitle
              ><span class="secondary--text black--text">
                <h2>{{ comment.author }}</h2>
              </span></v-card-subtitle
            >
            <v-card-text class="black--text">{{
              "Deficiência " + comment.condition
            }}</v-card-text>
            <v-card-text>{{ comment.text }}</v-card-text> </v-card
          ><br />
        </div>
      </v-col>
    </v-row>

    <v-card-title
      ><span class="black--text"><h2>Comunidades</h2></span></v-card-title
    >
    <v-card-subtitle
      ><h4>
        Este lugar foi muito citado nas seguintes comunidades:
      </h4></v-card-subtitle
    >
    
    <v-card elevation="3" color="blocos" @click="goToComunidade">
      <v-row class="text-center mt-1" justify="center">
        <v-col cols="1" md="1"></v-col>
        <v-col cols="2" md="2">
          <v-img class="rounded-circle pa-7" aspect-ratio="1" src="https://images.unsplash.com/photo-1517604931442-7e0c8ed2963c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=750&q=80"></v-img>
        </v-col>
        <v-col cols="9">
          <v-card-subtitle><span class="black--text"><h3>Lugares bonitos em SP</h3></span></v-card-subtitle>        
        </v-col>
      </v-row>
    </v-card>

  </v-card>
</template>

<script>
export default {
  data: () => ({
      comment: "",
      comments: [
        
      ],
    }),

  async asyncData({ params, query, $axios }) {
    const data = await $axios.$get(`/place/${params.id}`);
    return {
      ...data,
      address: query.address,
      name: query.name,
      accessibility: (query.accessibility || "").split(",").filter(e => e),
      image: query.image,
    };
  },
  methods: {
    goToMapa() {
      // console.log(this.address);
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
    },
    sendMessage(){
      // console.log("AAAAAAAAAAAAAAAAAAAAAA")
      this.$data.comments.unshift({
        text:this.$data.comment,
        author:"Fátima",
        condition: ['Visual'],
      })
    }
  },
};
</script>
        