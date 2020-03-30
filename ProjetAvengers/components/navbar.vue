<template>
  <nav>
    <v-content>
      <v-app-bar app fixed class="blue darken-2">
        <v-tooltip bottom>
          <template v-slot:activator="{on}">
            <v-app-bar-nav-icon v-on="on" @click="drawerNav=!drawerNav"></v-app-bar-nav-icon>
          </template>
          <span>Navigation</span>
        </v-tooltip>
        <v-icon x-large color="white darken-1 white--background">mdi-angularjs</v-icon>
        <v-toolbar-title class="font-italic font-weight-medium display-1 white--text">Avengers !</v-toolbar-title>
        <v-spacer></v-spacer>
        <div class="text-center">
          <v-menu bottom
                  origin="top center"
                  transition="scale-transition"
          >
            <template v-slot:activator="{on}">
              <v-btn text class="gray" v-on="on">
                Menu
                <v-icon>mdi-arrow-down-drop-circle-outline</v-icon>
              </v-btn>
            </template>
            <v-list >
              <v-list-item v-for="(link,i) in navLinks" :key="i" nuxt :to="link.route">
                {{link.text}}
              </v-list-item>
            </v-list>
          </v-menu>
        </div>

        <v-tooltip bottom>
          <template v-slot:activator="{on}">
            <v-btn v-on="on" icon>
              <v-icon>mdi-magnify</v-icon>
            </v-btn>
          </template>
          <span>Recherche</span>
        </v-tooltip>

          <v-tooltip bottom>
            <template v-slot:activator="{on}">
              <v-btn v-on="on" icon @click="drawerUser=!drawerUser">
                <v-icon>mdi-account</v-icon>
              </v-btn>
            </template>
            <span>Utilisateur</span>
          </v-tooltip>
      </v-app-bar>
    </v-content>

    <v-navigation-drawer left app v-model="drawerNav" class="blue darken-2">
      <v-list>
        <h2 align="center">Navigation</h2>
        <v-list-item v-for="link in navLinks" :key="link.route" nuxt :to="link.route">
          <v-list-item-icon><v-icon>{{link.icon}}</v-icon></v-list-item-icon>
          <v-list-item-title>{{link.text}}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>



        <v-navigation-drawer right v-model="drawerUser" app class="blue darken-2">
          <v-list>
            <h2 align="center">Utilisateur</h2>
                  <v-list-item>
                    <connexion/>
                  </v-list-item>
                  <v-list-item>
                    <inscription/>
                  </v-list-item>
                </v-list>
        </v-navigation-drawer>
  </nav>
</template>

<script>
  import connexion from "./connexion";
  import inscription from "./inscription";
  export default {
    name: "navbar",
    components:{
      connexion,
      inscription
    },
    data(){
      return{
        drawerNav:false,
        drawerUser:false,
        navLinks:[
          {icon:'mdi-home', text:'Accueil', route:'/'},
          {icon:'mdi-account', text: 'Civils', route:'/civils'},
          {icon:'mdi-home-city', text: 'Organisations', route:'/organisations'},
          {icon:'mdi-star-circle-outline', text: 'Super heros', route:'/super_hero'},
          {icon:'mdi-emoticon-devil-outline', text:'Super vilains', route:'/super_vilains'},
          {icon:'mdi-alert-decagram', text:'Incidents', route:'/incidents'},
          {icon:'mdi-handshake', text:'Missions', route:'/missions'}
        ],
      }
    },
  }
</script>

<style scoped>

</style>
