<template>
  <v-container>
    <button @click="displayList=!displayList">Afficher la liste</button>
    <br>
    <ul v-if="displayList">
      <li v-for="user in users" :key="firstname">
        {{user.firstname}} {{user.lastname}} Age: {{user.age}} ans
      </li>
    </ul>
  </v-container>
</template>

<script>
    export default {
        name: "test",
      data(){
          return{
            displayList:false,
            users:[
              {firstname:"LEPAPE", lastname:"Rémy", age:"24" },
              {firstname:"RICHARD", lastname:"Quentin", age:"24" },
              {firstname:"BRAUSEM", lastname:"JB", age:"19" },
              {firstname:"VAXELAIRE", lastname:"Antoine", age:"26"}
            ]
            }
          }
    }
</script>

<style scoped>

</style>
