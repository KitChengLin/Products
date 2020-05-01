<template>
  <div v-if="data">
    <v-list-item>
      <v-list-item-content>
      <v-row>
        <v-col cols="12" md="2">
          <v-card color="grey darken-3" dark>
            <v-card-title>Orden: {{data.order.number}}
              <v-spacer></v-spacer>
              <v-tooltip bottom>
              <template v-slot:activator="{ on }">
                <v-btn v-on="on" class="ma-1" style="cursor: pointer;" color="primary lighten-1" fab xl-small dark @click="showaddproduct()"><v-icon large dark>mdi-cart-plus</v-icon></v-btn>
              </template>
              <span>Añadir producto</span>
            </v-tooltip>
            <v-tooltip bottom>
              <template v-slot:activator="{ on }">
                <v-btn v-on="on" class="ma-1" style="cursor: pointer;" color="green lighten-1" fab xl-small dark @click="showpayproduct()"><v-icon large dark>mdi-credit-card-outline</v-icon></v-btn>
              </template>
              <span>Pagar productos</span>
            </v-tooltip>
            </v-card-title>
          </v-card>
        </v-col>
        <v-col cols="12" md="10">
          <v-hover
            v-slot:default="{ hover }"
            open-delay="100"
          >
            <v-card v-if="products" :elevation="hover ? 8 : 1">
              <v-data-table
                :headers="headers"
                :items="products"
                :items-per-page="15"
                class="elevation-1">
                <template slot="item" slot-scope="props">
                <tr>
                  <td class="text-xs-right">{{props.item.sku}}</td>
                  <td class="text-xs-right">{{props.item.name}}</td>
                  <td class="text-xs-right">{{props.item.quantity}}</td>
                  <td class="text-xs-right">{{props.item.price}}</td>
                </tr>
                </template>
              </v-data-table>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
      </v-list-item-content>
    </v-list-item>
    <v-dialog v-model="addproduct" persistent max-width="600px">
      <AddProduct v-if="products" @close="addproduct = false"
      :products="products"
      >
      </AddProduct>
    </v-dialog>
  </div>
</template>

<script>
import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import AddProduct from './AddProducts'
 
Vue.use(VueAxios, axios)
  export default {
    name: 'Products',

    data () {
      return {
        headers: [
          { text: 'Sku', value: 'sku', sortable: false },
          { text: 'Nombre', value: 'name', sortable: false },
          { text: 'Cantidad', value: 'quantity', sortable: false },
          { text: 'Precio', value: 'price', sortable: false }
        ],
        data: null,
        addproduct: false,
        products: null,
        token: 'eyJhbGciOiJIUzUxMiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJkM2NIVUVibVJoc1EzeXhNbzV2VnliSTFzaDZCSDJZRCIsImlhdCI6MTU4NTkzMjYzNDU0OH0.tMSht_M3ryQl5IqCirhYR1gb8j3FQ26vILT4Qpx4XrdFz-zUmqbgFYiKTaZHPpB85etRIMhxVoZf6tOrHy0fnA'
      }
    },
    components: {
      AddProduct
    },
    mounted() {
      this.fetchproducts()
    },
    methods: {
      fetchproducts () {
        Vue.axios.get("https://eshop-deve.herokuapp.com/api/v2/orders/2117155815564", {
          headers: {
            Authorization: this.token
          }
        }).then((response) => {
          this.data=response.data
          this.products = this.data.order.items.map(function(data) { return {sku: data.sku, name: data.name, quantity: data.quantity, price: data.price}})
        })
      },
      showaddproduct () {
        this.addproduct = true
      },
      showpayproduct () {

      }
    }
  }
</script>
