<template>
  <v-container>
    <v-card>
      <v-card-title>
        <v-text-field
          v-model="search"
          label="Recherche"
          single-line
          hide-details
        ></v-text-field>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="superHero"
        :search="search"
        v-on:click:row="dialogSuperHero = !dialogSuperHero"
      >
        <template v-slot:body="{ items }">
          <tbody>
          <tr v-for="item in items" @click="superHeroId=(item.id)-1, dialogSuperHero=!dialogSuperHero">
            <td>{{item.nom}}</td>
            <td>{{item.prenom}}</td>
            <td>{{item.code_postal}}</td>
          </tr>
          </tbody>
        </template>
      </v-data-table>
    </v-card>

    <v-row justify="center">
      <v-dialog v-model="dialogSuperHero" persistent max-width="900px" v-on:click:outside="dialogSuperHero=false" v-if="superHeroId!=null">
        <v-card>
          <v-toolbar flat color="primary" dark>
            <v-toolbar-title>{{superHero[superHeroId].nom}}</v-toolbar-title>
          </v-toolbar>
          <v-tabs vertical>
            <v-tab>
              <v-icon left>mdi-account</v-icon>
              Informations
            </v-tab>
            <v-tab>
              <v-icon left>mdi-at</v-icon>
              Coordonnées
            </v-tab>
            <v-tab>
              <v-icon left>mdi-access-point</v-icon>
              Incidents
            </v-tab>

            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <p>{{superHero[superHeroId].civilite}} {{superHero[superHeroId].nom}} {{superHero[superHeroId].prenom}}</p>
                  <p>Née le {{superHero[superHeroId].date_de_naissance}}</p>
                  <p> Nationalitée : {{superHero[superHeroId].nationalite}}</p>
                  <p> Habite à {{superHero[superHeroId].ville}}</p>

                </v-card-text>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text>
                  <v-list>
                    <v-list-item-title class="text-center">Telephone</v-list-item-title>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-phone</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>Portable : {{superHero[superHeroId].telephone_portable}}</v-list-item-title>
                      </v-list-item-content>
                      <v-list-item-action>

                        <v-icon>mdi-message-text</v-icon>
                      </v-list-item-action>
                    </v-list-item>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-phone</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>Fixe : {{superHero[superHeroId].telephone_fixe}}</v-list-item-title>
                      </v-list-item-content>

                      <v-list-item-action>
                        <v-icon>mdi-message-text</v-icon>
                      </v-list-item-action>
                    </v-list-item>

                    <v-divider inset></v-divider>
                    <v-list-item-title class="text-center mt-2">Adresse</v-list-item-title>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-map-marker</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>{{superHero[superHeroId].numero_voie}} {{superHero[superHeroId].adresse}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-map-marker</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>{{superHero[superHeroId].code_postal}} {{superHero[superHeroId].ville}} {{superHero[superHeroId].pays}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list>
                </v-card-text>
              </v-card>
            </v-tab-item>
            <v-tab-item>
              <v-card flat>
                <v-card-text>

                </v-card-text>
              </v-card>
            </v-tab-item>
          </v-tabs>
        </v-card>
      </v-dialog>
    </v-row>
  </v-container>
</template>


<script>
  export default {
    data () {
      return {
        search: '',
        headers: [
          {
            text: 'Nom',
            align: 'start',
            filterable: false,
            value: 'nom',
          },
          { text: 'Pouvoir', value: 'prenom' },
          { text: 'Score de popularité', value: 'code_postal' },
        ],
        superHero: [],
        dialogSuperHero: false,
        superHeroId: null
      }
    },
    methods:{
      dialog(){
        console.log()
      }
    },
    mounted() {
      this.$axios.$get('http://localhost:8080/utilisateurs')
        .then(response => this.superHero=response)
        .catch(error => console.log(error))
    }
  }
</script>

<style scoped>

</style>
