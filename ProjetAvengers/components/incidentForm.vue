<template>
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
</template>

<script>

  export default {
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
        this.$refs.observer.validate()
      },
      clear(){
        this.name = '',
        this.email = '',
        this.select = null,
        this.checkbox = null,
        this.$refs.observer.reset()
      }
    }
  }
</script>

<style scoped>

</style>
