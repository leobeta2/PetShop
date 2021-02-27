<template>
  <div>
  <div v-for="item in product" v-bind:key="item.name">
    <v-card
    elevation="2"
    max-width="374">
    <v-img
      height="250"
      v-bind:src=item.photo
    ></v-img>
    <v-card-title>{{item.name}}</v-card-title>
    <v-card-subtitle>subtitle</v-card-subtitle>
    <v-card-text>{{item.description}}</v-card-text>
    <v-card-actions>actions</v-card-actions>
    </v-card>
  </div>
    
  </div>
</template>

<script>
import axios from "axios";

  export default {
    name: 'Products',
    data() {
      return {
        product: [],
        index: 0
      }
    },
    methods: {

    },
    created() {
            axios.get("http://sva.talana.com:8000/api/product/")
            .then(resp => {
                this.product = resp.data;
      });    
    }
  }
</script>
