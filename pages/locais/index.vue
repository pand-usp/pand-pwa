<template>
  <v-container>
    <CommonSearch @search="getPlaces" path="/place" />
    <LocalCard
      class="my-5"
      v-for="local in locais"
      v-on:click.native="goTo(local)"
      :key="local.name"
      :name="local.name"
      :accessibility="local.accessibility"
      :address="local.address"
      :imageUrl="local.imageURL"/>
  </v-container>
</template>

<script>

export default {
  data() {
    return {
      locais: [],
      filters: [],
    }
  },
  async asyncData({ $axios, query }) {
    await setTimeout(() => {}, 200)

    if (query && Object.keys(query).length === 0) {
      query = {
        q: '',
        filters: '',
      }
    }

    const filters = query.filters.split(',').filter(e => e);
    // console.log(filters)
    const response = await $axios.$get('/place', {
      params: {
        q: query.q,
        filters: query.filters
      }
    });
    // console.log({response})

    return {
      locais: response.filter(local => {
        return filters.reduce((result, e) => {
          console.log(local, result && local.accessibility[e])
          return result && local.accessibility[e];
        }, true)
      })
    }
  },
  methods: {
    async getPlaces({ content, filters }) {
      const response = await this.$axios.$get('/place', {
        params: {
          q: content,
          filters,
        }
      });
      this.locais = response;
    },
    goTo(local) {
      this.$router.push({ 
        path: `/locais/${local.id}`,
        query: {
          address: local.address,
          image: local.imageURL,
          accessibility: Object.keys(local.accessibility).filter(key => local.accessibility[key] === true).join(),
          name: local.name
        },
      });
    }
  },
}
</script>