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
        :items="superVilain"
        :search="search"
        v-on:click:row="dialogSuperVilain = !dialogSuperVilain"
      >
        <template v-slot:body="{ items }">
          <tbody>
          <tr v-for="item in items" @click="superVilainId=(item.id)-1, dialogSuperVilain=!dialogSuperVilain">
            <td>{{item.nom}}</td>
            <td>{{item.prenom}}</td>
            <td>{{item.code_postal}}</td>
          </tr>
          </tbody>
        </template>
      </v-data-table>
    </v-card>

    <v-row justify="center">
      <v-dialog v-model="dialogSuperVilain" persistent max-width="900px" v-on:click:outside="dialogSuperVilain=false" v-if="superVilainId!=null">
        <v-card>
          <v-toolbar flat color="primary" dark>
            <v-toolbar-title>{{superVilain[superVilainId].nom}}</v-toolbar-title>
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
                  <p>{{superVilain[superVilainId].civilite}} {{superVilain[superVilainId].nom}} {{superVilain[superVilainId].prenom}}</p>
                  <p>Née le {{superVilain[superVilainId].date_de_naissance}}</p>
                  <p> Nationalitée : {{superVilain[superVilainId].nationalite}}</p>
                  <p> Habite à {{superVilain[superVilainId].ville}}</p>

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
                        <v-list-item-title>Portable : {{superVilain[superVilainId].telephone_portable}}</v-list-item-title>
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
                        <v-list-item-title>Fixe : {{superVilain[superVilainId].telephone_fixe}}</v-list-item-title>
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
                        <v-list-item-title>{{superVilain[superVilainId].numero_voie}} {{superVilain[superVilainId].adresse}}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>

                    <v-list-item @click="">
                      <v-list-item-action>
                        <v-icon>mdi-map-marker</v-icon>
                      </v-list-item-action>

                      <v-list-item-content>
                        <v-list-item-title>{{superVilain[superVilainId].code_postal}} {{superVilain[superVilainId].ville}} {{superVilain[superVilainId].pays}}</v-list-item-title>
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
          { text: 'Score de popularité', value: 'code_postal' }
        ],
        superVilain: [],
        dialogSuperVilain: false,
        superVilainId: null
      }
    },
    methods:{
      dialog(){
        console.log()
      }
    },
    mounted() {
      this.$axios.$get('http://localhost:8080/utilisateurs')
        .then(response => this.superVilain=response)
        .catch(error => console.log(error))
    }
  }
</script>

<style scoped>

</style>
