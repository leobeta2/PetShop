<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <h2>Pets Shop</h2>
      </div>
      <v-btn v-for="item in category" v-bind:key="item.id"
        text
        @click="typeCategory(item.order)"
      >
        <span class="mr-2">{{item.name}}</span>
      </v-btn>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
      <Products
        :category = order
      />
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import Products from './components/Products';


export default {
  name: 'App',

  components: {
    Products,
  },

  data: () => ({
    order:"1",
    category: null
  }),
  methods: {
      typeCategory(order) {
        this.order = order.toString();
      }
    },
      created() {
            axios.get("http://sva.talana.com:8000/api/product-category/")
            .then(resp => {
                this.category = resp.data;
      });    
    }
};
</script>

