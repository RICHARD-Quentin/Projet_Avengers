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
        :items="civils"
        :search="search"
        v-on:click:row="dialogCivil=!dialogCivil"
        >
        <template v-slot:body="{ items }">
        <tbody>
        <tr v-for="item in items" @click="civilId=(item.id)-1, dialogCivil=!dialogCivil">
          <td>{{item.civilite}}</td>
          <td>{{item.nom}}</td>
          <td>{{item.prenom}}</td>
          <td>{{item.code_postal}}</td>
          <td>{{item.ville}}</td>
          <td>{{item.pays}}</td>
        </tr>
        </tbody>
        </template>
      </v-data-table>
    </v-card>

    <v-row justify="center">
      <v-dialog v-model="dialogCivil" persistent max-width="900px" v-on:click:outside="dialogCivil=false" v-if="civilId!=null">
        <v-card>
          <v-toolbar flat color="primary" dark>
            <v-toolbar-title>{{civils[civilId].civilite}} {{civils[civilId].nom}} {{civils[civilId].prenom}}</v-toolbar-title>
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
                  <p>{{civils[civilId].civilite}} {{civils[civilId].nom}} {{civils[civilId].prenom}}</p>
                  <p>Née le {{civils[civilId].date_de_naissance}}</p>
                  <p> Nationalitée : {{civils[civilId].nationalite}}</p>
                  <p> Habite à {{civils[civilId].ville}}</p>

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
                        <v-list-item-title>Portable : {{civils[civilId].telephone_portable}}</v-list-item-title>
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
                        <v-list-item-title>Fixe : {{civils[civilId].telephone_fixe}}</v-list-item-title>
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
                        <v-list-item-title>{{civils[civilId].numero_voie}} {{civils[civilId].adresse}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-map-marker</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>{{civils[civilId].code_postal}} {{civils[civilId].ville}} {{civils[civilId].pays}}</v-list-item-title>
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
            text: 'Civilite',
            align: 'start',
            filterable: false,
            value: 'civilite',
          },
          { text: 'Nom', value: 'nom' },
          { text: 'Prenom', value: 'prenom' },
          { text: 'Code Postal', value: 'code_postal' },
          { text: 'Ville', value: 'ville' },
          { text: 'Pays', value: 'pays' },
        ],
        civils: [],
        dialogCivil: false,
        civilId: null
      }
    },
    methods:{
      dialog(){
        console.log()
      }
    },
    mounted() {
      this.$axios.$get('http://localhost:8080/utilisateurs')
        .then(response => this.civils=response)
        .catch(error => console.log(error))
    }
  }
</script>

<style scoped>

</style>
