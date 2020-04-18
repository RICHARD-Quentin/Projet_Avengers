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
        :items="organisations"
        :search="search"
        v-on:click:row="dialogOrganisation = !dialogOrganisation"
      >
        <template v-slot:body="{ items }">
          <tbody>
          <tr v-for="item in items" @click="organisationId=(item.id)-1, dialogOrganisation=!dialogOrganisation">
            <td>{{item.nom}}</td>
            <td>{{item.prenom}}</td>
            <td>{{item.ville}}</td>
            <td>{{item.pays}}</td>
            <td>{{item.code_postal}}</td>
          </tr>
          </tbody>
        </template>
      </v-data-table>
    </v-card>

    <v-row justify="center">
      <v-dialog v-model="dialogOrganisation" persistent max-width="900px" v-on:click:outside="dialogOrganisation=false" v-if="organisationId!=null">
        <v-card>
          <v-toolbar flat color="primary" dark>
            <v-toolbar-title>{{organisations[organisationId].nom}}</v-toolbar-title>
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
                  <p>{{organisations[organisationId].civilite}} {{organisations[organisationId].nom}} {{organisations[organisationId].prenom}}</p>
                  <p>Née le {{organisations[organisationId].date_de_naissance}}</p>
                  <p> Nationalitée : {{organisations[organisationId].nationalite}}</p>
                  <p> Habite à {{organisations[organisationId].ville}}</p>

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
                        <v-list-item-title>Portable : {{organisations[organisationId].telephone_portable}}</v-list-item-title>
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
                        <v-list-item-title>Fixe : {{organisations[organisationId].telephone_fixe}}</v-list-item-title>
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
                        <v-list-item-title>{{organisations[organisationId].numero_voie}} {{organisations[organisationId].adresse}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-map-marker</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>{{organisations[organisationId].code_postal}} {{organisations[organisationId].ville}} {{organisations[organisationId].pays}}</v-list-item-title>
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
          { text: 'Président', value: 'prenom' },
          { text: 'Ville', value: 'ville' },
          { text: 'Pays', value: 'pays' },
          { text: 'Nombre de membres', value: 'code_postal' },
        ],
        organisations: [],
        dialogOrganisation: false,
        organisationId: null
      }
    },
    methods:{
      dialog(){
        console.log()
      }
    },
    mounted() {
      this.$axios.$get('http://localhost:8080/utilisateurs')
        .then(response => this.organisations=response)
        .catch(error => console.log(error))
    }
  }
</script>

<style scoped>

</style>
