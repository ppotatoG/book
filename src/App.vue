<template>
  <v-app>
    <v-main>
      <HelloWorld/>
    </v-main>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import Vue from 'vue'
import 'vuetify/dist/vuetify.min.css'

import Vuetify from 'vuetify'

Vue.use(Vuetify)

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
};
</script>
