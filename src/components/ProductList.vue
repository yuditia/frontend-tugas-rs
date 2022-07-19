<template>
  <div
    class="card mt-5 shadow"
    style="width: 16rem; margin: 5px; padding: 10px"
    v-for="product in products"
    :key="product.id"
  >
    <img
      :src="'http://127.0.0.1:8000/storage/' + product.image"
      class="card-img-top"
      alt="{{ product.name }}"
    />
    <div class="card-body">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text">Stock: {{ product.stock }}</p>
      <p class="card-text">Price: {{ product.price }}</p>
      <a @click="showcard" class="btn btn-primary">Go somewhere</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { onMounted, ref } from "vue";

export default {
  methods: {
    showcard() {
      return alert("mantab");
    },
  },
  setup() {
    let products = ref([]);

    onMounted(() => {
      axios
        .get("http://127.0.0.1:8000/api/v1/products")
        .then((result) => {
          products.value = result.data.data;
        })
        .catch((err) => {
          console.log(err.response);
        });
    });

    return {
      products,
    };
  },
};
</script>
