<template>
  <div>
    <h2>Cari Produk</h2>
    <input
      v-model="searchTitle"
      type="text"
      placeholder="Cari berdasarkan judul produk"
      @keyup.enter="searchProducts()"
    />
    <button @click="searchProducts()">Cari</button>

    <div v-if="products.length > 0">
      <h3>Produk yang Ditemukan</h3>
      <ul>
        <li v-for="product in products" :key="product.id">
          {{ product.title }} - {{ product.price }}
        </li>
      </ul>
    </div>

    <div v-if="products.length === 0 && isSearching">
      <p>Tidak ada produk yang ditemukan</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      searchTitle: "",
      products: [],
      isSearching: false,
    };
  },
  methods: {
    searchProducts() {
      this.isSearching = true;
      axios
        .get(`https://dummyjson.com/products/search?q=${this.searchTitle}`)
        .then((response) => {
          const sortedProducts = response.data.products.sort(
            (a, b) => a.price - b.price
          );
          this.products = sortedProducts.slice(0, 3);
          console.log(this.products);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
