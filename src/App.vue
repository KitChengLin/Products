<template>
  <v-app>
    <v-app-bar
      app
      class="grey darken-3"
      dark
    >
      <v-icon class="display-1">mdi-cart-arrow-down</v-icon>
      <span class="display-1 font-weight-bold">Products</span>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <Products/>
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
