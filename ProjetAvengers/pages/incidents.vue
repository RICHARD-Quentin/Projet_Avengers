<template>
  <v-container>
<!--  <v-card>
    <v-toolbar flat>
      <template v-slot:extension>
        <v-tabs
          v-model="tabs"
          fixed-tabs
        >
          <v-tabs-slider></v-tabs-slider>
          <v-tab
            href="#mobile-tabs-5-1"
            class="gray&#45;&#45;text">
          <v-icon>mdi-clipboard-list-outline</v-icon> Voir les derniers incidents

          </v-tab>

          <v-tab
            href="#mobile-tabs-5-2"
            class="gray&#45;&#45;text"
          >
            <v-icon>mdi-phone</v-icon> Soumettre un incident
          </v-tab>

          <v-tab
            href="#mobile-tabs-5-3"
            class="gray&#45;&#45;text"
          >
            <v-icon>mdi-progress-check</v-icon> Traitement de mes incidents
          </v-tab>
        </v-tabs>
      </template>
    </v-toolbar>

    <v-tabs-items v-model="tabs">
      <v-tab-item
        v-for="i in content"
        :key="i"
        :value="'mobile-tabs-5-' + i"
      >
        <v-card flat>
    <v-card-text>{{i.balise}}</v-card-text>
    </v-card>
    </v-tab-item>
    </v-tabs-items>

    </v-card>-->
    <form>
      <v-text-field
        v-model="name"
        label="Name"
        required
      ></v-text-field>
      <v-text-field
        v-model="email"
        label="E-mail"
        required
      ></v-text-field>
      <v-select
        v-model="select"
        :items="items"
        label="Item"
        required
      ></v-select>
      <v-checkbox
        v-model="checkbox"
        label="Do you agree?"
        required
      ></v-checkbox>

      <v-btn class="mr-4" @click="submit">submit</v-btn>
      <v-btn @click="clear">clear</v-btn>
    </form>
  </v-container>
</template>

<script>
    export default {
        name: "incidents",
      data() {
        return{
          name: '',
          email: '',
          select: null,
          items: [
            'Item 1',
            'Item 2',
            'Item 3',
            'Item 4',
          ],
          checkbox: false,
        }
      },
      methods: {

        submit(){
        },
        clear(){
          this.name = '',
            this.email = '',
            this.select = null,
            this.checkbox = null
        }
      }
    }
</script>

<style scoped>

</style>
