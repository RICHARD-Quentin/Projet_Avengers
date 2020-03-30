<template>
  <v-row justify="center">
    <v-dialog v-model="dialogConnexion" persistent max-width="600px">
      <template v-slot:activator="{on}">
        <v-icon>mdi-login-variant</v-icon>
        <v-btn text v-on="on">

          Connexion
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">User Profile</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field label="Email*" required></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field label="Password*" type="password" required></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="red darken-1" text @click="dialogConnexion = false">Close</v-btn>
          <v-btn color="blue darken-1" text @click="dialogConnexion = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
    export default {
        name: "connexion",
      data(){
        return{
          dialogConnexion: false
        }
      }
    }
</script>

<style scoped>

</style>
