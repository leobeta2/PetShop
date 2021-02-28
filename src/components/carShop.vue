<template>
  <v-app> </v-app>
</template>

<script>
import axios from "axios";
import Products from "./components/Products";

export default {
  name: "App",

  components: {
    Products,
  },

  data: () => ({
    order: "1",
    category: null,
  }),
  methods: {
    typeCategory(order) {
      this.order = order.toString();
    },
  },
  created() {
    axios
      .get("http://sva.talana.com:8000/api/product-category/")
      .then((resp) => {
        this.category = resp.data;
      });
  },
};
</script>
