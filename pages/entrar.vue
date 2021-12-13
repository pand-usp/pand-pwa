<template>
  <v-container>
    <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6" align-items="center">
        <v-card light class="py-4 d-flex flex-column" align="center">
          <v-card-title class="headline justify-center">
            <h2>Login</h2>
          </v-card-title>
          
          <v-card-actions class="d-flex flex-column" align-items="center" width="auto">
            <v-row>
              <br/>
                <v-text-field
                  v-model="nickname"
                  label="Apelido ou E-mail"
                  required
                ></v-text-field>
            </v-row>

            <br/>
            <v-row>
              <v-text-field
                v-model="password"
                append-icon="mdi-eye-off"
                type="password"
                label="Senha"
                required
              ></v-text-field>
            </v-row>

            <div style="display:flex " class="mt-4">
              <v-btn
                class="mr-4 text-xs-center black--text" 
                color="primary"
                elevation="2"
                nuxt
                large
                to="/locais"
              >
              Entrar
            </v-btn>

            <v-btn
                class="text-xs-center white--text" 
                color="secondary"
                elevation="2"
                nuxt
                large
                to="/registrar"
              >
              Registrar
            </v-btn>
            </div>

            

          </v-card-actions>

        </v-card>
          <!-- fazer uma gambiarra p deixar bonito só, ja q n vamos usar -->

      </v-col>
    </v-row>
  </v-container>
</template>

