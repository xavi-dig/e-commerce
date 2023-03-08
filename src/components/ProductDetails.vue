<template>
  <div>
    <h2>{{ product.name }} - {{ product.price }}</h2>
    <p>{{ product.description }}</p>
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>

<script>
import { computed, ref } from "vue";
import { supabase } from "../supabase";

export default {
  name: "ProductDetails",
  props: {
    id: {
      type: Number,
      required: true,
    },
  },
  async setup(props) {
    const product = ref({});

    const { data, error } = await supabase
      .from("products")
      .select("*")
      .eq("id", props.id)
      .single();

    if (error) {
      console.error(error);
    } else {
      product.value = data;
    }

    const addToCart = () => {
      // add the product to the cart
    };

    return {
      product,
      addToCart,
    };
  },
};
</script>
