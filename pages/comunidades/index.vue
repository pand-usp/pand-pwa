<template>
  <v-container>
    <!-- <CommonSearch @search="getCommunities" path="/community" /> -->
     <CommonSearch />
    <ComunidadeListItem
      v-for="comunidade in comunidades"
      v-on:click.native="goTo(comunidade)"
      :key="comunidade.id"
      :name="comunidade.name"
      :description="comunidade.description"
      :imgPath="comunidade.imgPath"
    />
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      comunidades: [
      {
        id: 1,
        name: "Lugares bonitos em SP",
        description: "olosko",
        imgPath: "https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/MASP_Brazil.jpg/1920px-MASP_Brazil.jpg"
      },
      {
        id: 2,
        name: "Jogos",
        description: "olosko",
        imgPath: "https://www.baressp.com.br/bares/fotos2/ludus-luderia-baressp-1-min.jpg"
      },
      {
        id: 3,
        name: "Cinemas e filmes acessíveis",
        description: "olosko",
        imgPath: "https://blogtendadosaber.com.br/wp-content/uploads/2019/10/MEC-vai-incentivar-cinemas-acess%C3%ADveis-a-surdos-cegos-e-autistas-nas-unidades-da-Federa%C3%A7%C3%A3o.jpeg"
      },
      {
        id: 4,
        name: "Lugares acessíveis com música",
        description: "olosko",
        imgPath: "https://www.ricardoshimosakai.com.br/wp-content/uploads/2011/09/Balada-multisensorial-para-surdos-do-clube-Sencity-vem-ao-Brasil-em-setembro.jpg"
      },
      {
        id: 5,
        name: "Ar livre",
        description: "olosko",
        imgPath: "https://www.melhoresdestinos.com.br/wp-content/uploads/2019/02/passagens-aereas-sao-paulo-capa2019-04.jpg"
      },
      {
        id: 6,
        name: "Oportunidades de emprego para deficientes",
        description: "olosko",
        imgPath: "https://empregosecarreiras.opovo.com.br/wp-content/uploads/2019/10/Sine-abre-80-vagas-de-emprego-para-pessoas-com-defici%C3%AAncia.jpg"
      },
      ],
    };
  },
  // async asyncData({ $axios, query }) {
  //   await setTimeout(() => {}, 200)
  //   const response = await $axios.$get("/community", {
  //     params: {
  //       q: query.q,
  //       filters: query.filters,
  //     },
  //   });

  //   return {
  //     : response,
  //   };
  // },
  methods: {
    async getCommunities({ content, filters }) {
      const response = await this.$axios.$get("/community", {
        params: {
          q: content,
          filters,
        },
      });
      this.comunidades = response;
    },
    goTo(comunidade) {
      this.$router.push({
        path: `/comunidades/${comunidade.id}`,
        query: {
          name: comunidade.name,
          description: comunidade.description,
          imgPath: comunidade.imgPath,
        },
      });
    },
  },
};
</script>
