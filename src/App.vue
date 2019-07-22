<template>
  <v-app>
    <v-toolbar color="indigo" dark fixed app>
      <v-toolbar-title>Student List</v-toolbar-title>
    </v-toolbar>

    <v-content>
      <Index/>
    </v-content>

     <v-footer color="indigo" app>
      <span class="white--text">&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
import Index from './components/Index'

export default {
  name: 'App',
  components: {
    Index
  },
   data: () => ({
      drawer: null
    }),
}
</script>
