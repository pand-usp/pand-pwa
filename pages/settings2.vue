<template>
  <v-container>
    <v-row align="center" justify="space-around" class="pt-8">
    <v-col cols="12" sm="8" md="6" align-items="center">
        <v-card-text align="center" class="title font-weight-bold pt-0 black--text"
        ><h1>Configurações</h1></v-card-text
        >


        <v-card-actions class="d-flex flex-column" align-items="center" width="auto">
        <v-row>
            <v-text-field
                v-model="nickname"
                label="Apelido"
                required
                outlined
            ></v-text-field>
        </v-row>

        <v-row>
            <v-text-field
                color="purple"
                v-model="teste"
                label="teste"
                required
                outlined
            ></v-text-field>
        </v-row>

        </v-card-actions>

    </v-col>
    </v-row>
  </v-container>
</template>

