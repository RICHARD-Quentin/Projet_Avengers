<template>
  <v-app>
    <navbar/>
    <v-content>
      <nuxt/>
    </v-content>
  </v-app>
</template>

<script>
  import navbar from "../components/navbar";
export default {
  components:{
    navbar
  }
}
</script>
