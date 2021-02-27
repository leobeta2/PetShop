<template>
  <div>
    <v-card
      v-for="item in product" v-bind:key="item.name"
      class="mx-auto"
      :class="$style.cardProduct"
      max-width="345"
      elevation="2"
    >
    <v-img
      v-bind:src=item.photo
    ></v-img>
    <div :class="$style.title">
      <v-img :class="$style.icon"
      v-bind:src=item.attributes[0].icon
    ></v-img>
      <v-card-title>{{item.name}}</v-card-title>
    </div>
    <v-card-text>
      <div :class="$style.espaciado"> 
        <h3><b>Precio: ${{item.price}}</b></h3>
        <p>
        stock: {{item.stock}}
        </p></div>
        <div :class="$style.espaciado">
          <p>Categoría: {{item.category.name}}</p>
          <p>Mascota: {{item.attributes[0].name}}</p>
        </div>
    </v-card-text>

    <v-card-actions>
      <v-btn
        text
        color="teal accent-4"
        @click="revealText(item.id)"
      >
        Leer más...
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <v-card
        v-if="showCard(item.id)"
        class="transition-fast-in-fast-out"
        :class="$style.cardReveal"
        style="height: 100%;"
      >
        <v-card-text class="pb-0">
          <p class="display-1 text--primary">
            {{item.abstract}}
          </p>
          <p>{{item.description}}</p>
        </v-card-text>
        <v-card-actions class="pt-0">
          <v-btn
            text
            color="teal accent-4"
            @click="revealText(item.id)"
          >
            Cerrar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-expand-transition>
  </v-card>
  </div>
</template>

<script>
import axios from "axios";

  export default {
    name: 'Products',
    data() {
      return {
        product: [],
        index: 0,
        cardId: -1,
      }
    },
    methods: {
      revealText(id){
        console.log('reveal text'+ id);
        if(this.cardId !== id){
              this.cardId = id;
        }else{
          this.cardId = -1;
        }
      }, 
      showCard(id){
        console.log('otra vez'+ id);
        return this.cardId === id ? true : false;
      },
    },
    computed: {

    },
    created() {
            axios.get("http://sva.talana.com:8000/api/product/")
            .then(resp => {
                this.product = resp.data;
      });    
    }
  }
</script>

<style lang="scss" module>

.espaciado {
  display: flex;
  justify-content: space-between;
  padding-right: 30px;
}

.title {
  display: flex;
  flex-direction: row;
}

.icon {
  width: 10px;
}

.cardReveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}

.cardProduct {
  padding-top: 10px;
}

</style>


