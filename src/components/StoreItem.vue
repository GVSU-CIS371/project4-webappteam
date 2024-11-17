<template>
<!--your answer-->
<v-row>
<v-col v-for="product in filteredProducts" :key="product.id" cols="12" sm="6" md="4" lg="3">
<v-card >
  <v-card-title>
    {{ product.data.name }}
  </v-card-title>
  <v-card-subtitle>
    {{ product.data.rating }} {{ product.data.price }} {{ product.data.stock }}
  </v-card-subtitle>
  <v-img :src="product.data.image" height="200px"></v-img>
  <v-card-text>
    {{ product.data.description }}
  </v-card-text>
</v-card>
</v-col>
</v-row>
</template>

<script lang="ts" setup>
// your answer
import { useProductStore } from '../stores/ProductStore';
import {ref, computed} from "vue";

const props = defineProps({
  category: {
    type: String,
    required: true,
  },
});

let productStore = useProductStore();
productStore.init();

let productList = ref(productStore.products);
let filteredProducts: any;

if(props.category === "none"){
  filteredProducts = productList
}else if(props.category === "rating"){
  filteredProducts = computed(() => {
    return productStore.filterByRating(4.5);
  });
}else{
filteredProducts = computed(() => {
  return productStore.filterByCategory(props.category);
});
}
</script>
