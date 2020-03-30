<template>
  <div id="app">
    <li v-for="infos in info">{{ infos.civilite }} {{ infos.nom }} {{ infos.prenom }}</li>
  </div>
</template>

<script>
    import axios from "../../ProjetJava/.nuxt/axios";

    export default {
     data(){
       return{
         info:null
       }
     },
      mounted() {
        this.$axios.$get('http://localhost:8080/utilisateurs')
          .then(response => {this.info = response })
          .catch(error => console.log(error))
      }


    }
</script>

<style scoped>

</style>
