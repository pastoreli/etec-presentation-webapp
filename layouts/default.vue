<template>
  <v-app class="pet-app">
    <toolbar @shareFriend="showDialog = true" />
    <v-content class="page">
      <nuxt />
      <dialog-default 
        v-model="showDialog">
        <register-pet 
          @close="showDialog = false"
          @registerPet="registerPet" />
      </dialog-default>
    </v-content>
  </v-app>
</template>

<script>
import { Toolbar } from  '@/components/Partials';
import RegisterPet from '@/components/RegisterPet';

import { APIPets } from '@/API/endpoints';
export default {
  components: {
    Toolbar,
    RegisterPet
  },
  data: () => ({
    showDialog: false
  }),
  methods: {
    async registerPet(pet) {
      await APIPets.registerPet(pet)
      .then(res => {
        console.log('pet', res);
        this.$nuxt.$emit('setNewPet', pet);
      })
      .catch(error => {

      })
    }
  },
}
</script>
