<template>
  <v-row justify="center">
    <v-dialog v-model="dialogInscription" persistent max-width="600px" v-on:click:outside="dialogInscription=false">
      <template v-slot:activator="{on}">
        <v-icon>mdi-account-plus</v-icon>
        <v-btn text v-on="on">Inscription</v-btn>
      </template>
      <v-card
        class="mx-auto"
        max-width="600"
      >
        <v-card-title class="title font-weight-regular justify-space-between">
          <span>{{ currentTitle }}</span>
          <v-avatar
            color="primary lighten-2"
            class="subheading white--text"
            size="24"
            v-text="step"
          ></v-avatar>
        </v-card-title>

        <v-window v-model="step">
          <v-window-item :value="1">
            <v-card-text>
              <v-text-field
                label="Email"
                value="Votre email"
              ></v-text-field>
              <span class="caption grey--text text--darken-1">
            Cet email vous servira de nom de compte pour l'application
          </span>
            </v-card-text>
          </v-window-item>

          <v-window-item :value="2">
            <v-card-text>
              <v-text-field
                label="Mot de passe"
                type="password"
              ></v-text-field>
              <v-text-field
                label="Confirmez votre mot de passe"
                type="password"
              ></v-text-field>
              <span class="caption grey--text text--darken-1">
            Merci d'entrer un mot de passe
          </span>
            </v-card-text>
          </v-window-item>

          <v-window-item :value="3">
            <v-card-text>
              <v-text-field
                label="Nom"
                type="text"
              ></v-text-field>
              <v-text-field
                label="Prenom"
                type="text"
              ></v-text-field>
              <span class="caption grey--text text--darken-1">
            Merci d'entrer vos nom et prenom
          </span>
            </v-card-text>
          </v-window-item>
        </v-window>

        <v-divider></v-divider>

        <v-card-actions>
          <v-btn
            v-if="step !== 1"
            text
            @click="step--"
          >
            Précédent
          </v-btn>
          <v-spacer></v-spacer>
          <v-btn
            v-if="step !== 3"
            color="primary"
            depressed
            @click="step++"
          >
            Suivant
          </v-btn>


          <v-btn
            v-if="step===3"
            color="primary"
            depressed
            @click="dialogInscription=false, step=1"
          >
            Envoyer
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
  export default {
    name: "inscription",
    data(){
      return{
        dialogInscription: false,
        step: 1
      }
    },
    computed: {
      currentTitle () {
        switch (this.step) {
          case 1: return 'Email'
          case 2: return 'Créer un mot de passe'
          default: return 'Compte crée !'
        }
      },
    }
  }
</script>

<style scoped>

</style>
