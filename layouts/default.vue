<template>
  <v-app :style="{background: this.$vuetify.theme.themes[theme].background}">
    <v-navigation-drawer
      class="teal lighten-5"
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      right
      fixed
      app
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          @click="checkLogout"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon color="black">{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" class="black--text" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      class="primary"
      :clipped-left="clipped"
      fixed
      app
    >
      <v-btn
        icon
        @click.stop="goBack"
      >
        <v-icon>mdi-{{ `chevron-left` }}</v-icon>
      </v-btn>
      <v-spacer/>
      <div v-if="showUser" class="secondary rounded-circle bold" style="width:32px;height:32px;justify-content:center;display:flex;"> 
        <button v-on:click="goToPerfil">I</button>
        <p class="mt-4 font-weight-bold" style="align-self:center;"></p> 
      </div>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <!-- n sei se vamos colocar isso aqui -->
      <v-toolbar-title v-text="title" />
    </v-app-bar>
    <v-main>
      <Nuxt />
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      showUser: true,
      items: [
        {
          icon: 'mdi-magnify',
          title: 'Buscar',
          to: '/'
        },
        {
          icon: 'mdi-map-marker',
          title: 'Locais',
          to: '/locais'
        },
        {
          icon: 'mdi-account-group',
          title: 'Comunidade',
          to: '/comunidade'
        },
        {
          icon: 'mdi-cog-outline',
          title: 'Configuração',
          to: '/settings'
        },
        {
          icon: 'mdi-plus-circle',
          title: 'Adicionar local',
          to: '/addLocal'
        },
        
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: ''
    }
  },
  methods: {
    goBack() {
      this.$router.go(-1);
    },
    checkLogout(e) {
      if (e.target.innerHTML === 'Sair') {
        this.$data.items.pop()
        this.$data.items.push({
          icon: 'mdi-login-variant',
          title: 'Entrar',
          to: '/entrar'
        });
        this.$data.showUser = false;
      }
    },
    goToPerfil({content, filters}) {
      this.$router.push({ 
        path: `/perfil`,
      });
    },
  },
  computed:{
    theme(){
      return (this.$vuetify.theme.dark) ? 'dark' : 'light'
    }
  }
}
</script>

<style scoped>
v-app {
  font-family: 'Montserrat', sans-serif;
}
</style>