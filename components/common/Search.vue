<template>
  <v-container class="pa-2 mb-8">
    <v-row>
      <v-col cols="12" align="center">
        <p class="mb-0 pb-0 black--text"> Qual(is) tipos de acessibilidade você deseja? </p>
      </v-col>
    </v-row>

    <v-row justify="center">
      <v-col class="pt-0 mb-4" cols="10">
        <div class="d-flex justify-center">
          <v-chip-group
            multiple
            v-model="filters"
            active-class="secondary"
          >
            <v-chip value="fisica">Física</v-chip>
            <v-chip value="auditiva">Auditiva</v-chip>
            <v-chip value="visual">Visual</v-chip>
          </v-chip-group>
        </div>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="12" align="center">
        <v-text-field
          class="search-field"
          filled
          v-model="content"
          placeholder="Buscar..."
          background-color="blocos"
          rounded
          hide-details
          append-icon="mdi-magnify"
          append-outer-icon="mdi-microphone-outline"
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col cols="5" align="center">
        <v-btn
          class="black--text font-weight-bold"
          width="120"
          large
          rounded
          elevation="4"
          color="blocos"
        >
          Filtro
        </v-btn>
      </v-col>
      <v-col cols="5" align="center">
        <v-btn
          class="black--text"
          width="120"
          large
          rounded
          elevation="4"
          color="primary"
          v-on:click="search"
        >
          Pesquisar
        </v-btn>
      </v-col>
    </v-row>
  </v-container> 
</template>

<script>
export default {
  data() {
    return {
      content: "",
      filters: [],
    }
  },
  methods: {
    search() {
      this.$emit('search', { content: this.content, filters: this.filters });
    }
  }
}
</script>