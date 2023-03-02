<template>
  <div>
    <section class="home-section mt-5" id="home">
      <div class="container">
        <div class="row d-flex align-items-center">
          <div class="col-lg-6">
            <img
              class="img-fluid"
              src="https://images.unsplash.com/photo-1449247666642-264389f5f5b1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1469&q=80"
              alt=""
            />
          </div>
          <div class="col-lg-6">
            <div class="data">
              <h1>Cari barang termurah dan termudah disini</h1>
              <p>
                Lorem ipsum dolor sit amet consectetur adipisicing elit.
                Voluptate asperiores facere quod debitis eveniet consectetur
                ipsa in veritatis minus corrupti sed qui porro aliquid sunt, eos
                consequatur modi optio a!
              </p>
              <a href="" class="btn btn-primary">Cari Barang</a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section class="barang-section mt-5" id="barang">
      <div class="container">
        <div class="header">
          <h2 class="text-center">Mulai Cari</h2>
          <input
            type="text"
            v-model="searchTitle"
            class="form-control"
            placeholder="Sepatu olahraga"
          />
          <button @click="searchProducts()" class="btn btn-primary mt-3">
            Cari
          </button>
        </div>
        <div class="hasil mt-5">
          <p class="text-muted">Hasil Pencarian</p>
          <div class="grid row gap-4 row-cols-4">
            <div class="card col" v-for="product in products" :key="product.id">
              <div class="card-body">
                <img v-bind:src="product.thumbnail" alt="" class="img-fluid" />
              </div>
              <div class="card-footer d-flex justify-content-between">
                <div class="">
                  <p>
                    <b>{{ product.title }}</b>
                  </p>
                  <h3>USD {{ product.price }}</h3>
                </div>
              </div>
            </div>
          </div>
          <div v-if="products.length === 0 && isSearching">
            <p>Tidak ada produk yang ditemukan</p>
          </div>
        </div>
      </div>
    </section>
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
