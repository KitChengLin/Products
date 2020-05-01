<template>
  <v-app>
    <v-app-bar
      app
      class="grey darken-3"
      dark
    >
      <v-icon class="display-1">mdi-cart</v-icon>
      <span class="display-1 font-weight-bold">Productos</span>
    <v-divider></v-divider>
    </v-app-bar>
    <v-content>
      <Products/>
      <v-footer 
      absolute
      class="font-weight-end grey darken-2"
      dark>
        <v-spacer></v-spacer>
        <div>&copy; {{ new Date().getFullYear() }} - <strong>kitchenglin</strong> </div>
      </v-footer>
    </v-content>
  </v-app>
</template>

<script>
import Products from './components/Products';

export default {
  name: 'App',

  components: {
    Products,
  },

  data: () => ({
    //
  }),
};
</script>
