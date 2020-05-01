<template>
  <v-form ref="form">
    <v-toolbar dark color="grey darken-3">
      <v-toolbar-title>Añadir nuevo producto</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn v-on="on" icon dark text @click="closeModal()">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </template>
        <span>Cerrar</span>
      </v-tooltip>
    </v-toolbar>
    <v-card>
      <v-list-item>
        <v-list-item-content>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="editedItem.sku"
              outlined
              clearable
              label="Sku"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="editedItem.name"
              outlined
              clearable
              label="Nombre"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="editedItem.quantity"
              outlined
              clearable
              label="Cantidad"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col cols="12" md="6">
            <v-text-field
              v-model="editedItem.price"
              outlined
              clearable
              label="Precio"
              :rules="[rules.required]"
            >
            </v-text-field>
          </v-col>
          <v-col>
            <v-layout align-begin justify-end>
              <v-btn dark color="grey darken-3" v-on:click="save"
                >Guardar</v-btn
              >
            </v-layout>
          </v-col>
        </v-list-item-content>
      </v-list-item>
    </v-card>
  </v-form>
</template>
<script>
export default {
  props: {
    products: {
      type: Array,
      default: () => {
        return "";
      }
    }
  },
  data() {
    return {
      edited: -1,
      editedItem: {
        sku: 0,
        name: "",
        quantity: 0,
        price: 0
      },
      defaultItem: {
        sku: 0,
        name: "",
        quantity: 0,
        price: 0
      },
      formHasErrors: false,
      rules: {
        required: value => !!value || "Requerido."
      }
    };
  },
  methods: {
    closeModal() {
      this.$emit("close");
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem);
        this.edited = -1;
        this.$refs.form.reset();
      }, 300);
    },
    save() {
      if (
        this.editedItem.sku > 0 &&
        this.editedItem.name !== "" &&
        this.editedItem.quantity > 0 &&
        this.editedItem.price > 0
      ) {
        if (this.edited > -1) {
          Object.assign(this.products[this.edited], this.editedItem);
        } else {
          this.products.push(this.editedItem);
        }
        this.closeModal();
        this.$swal(
          "Cambios guardados",
          "Se ha añadido un nuevo producto",
          "success"
        );
      } else {
        this.$swal("Ha ocurrido un error!", "Complete el formulario", "error");
      }
    }
  }
};
</script>
