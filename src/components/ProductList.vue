<template>
  <div>
    <input type="text" v-model="searchTerm" placeholder="Search..." />
    <ul>
      <li
        v-for="product in filteredProducts"
        :key="product.id"
        @click="selectProduct(product)"
      >
        {{ product.name }} - {{ product.price }}
      </li>
    </ul>
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
import { supabase } from "../supabase";

export default {
  name: "ProductList",
  data() {
    return {
      products: [],
      searchTerm: "",
    };
  },
  computed: {
    filteredProducts() {
      return this.products.filter((product) =>
        product.name.toLowerCase().includes(this.searchTerm.toLowerCase())
      );
    },
  },
  methods: {
    selectProduct(product) {
      this.$router.push({ name: "product", params: { id: product.id } });
    },
  },
  setup() {
    const products = ref([]);

    watchEffect(async () => {
      const { data, error } = await supabase.from("products").select("*");

      if (error) {
        console.error(error);
      } else {
        products.value = data;
      }
    });

    return {
      products,
    };
  },
};
</script>
