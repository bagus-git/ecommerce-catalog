<template>
  <div>
    <h1>Data Produk</h1>
    <ul>
      <!-- setiap objek produk dalam array products akan ditampilkan dalam bentuk elemen list -->
      <li v-for="product in products" :key="product.id">{{ product.title }} - {{ product.price }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.loadProducts();
  },
  methods: {
    async loadProducts() {
      for (let i = 1; i <= 20; i++) {
        // untuk mengambil data produk dari API Fake Store
        const response = await fetch(`https://fakestoreapi.com/products/${i}`);
        const data = await response.json();
        // hanya produk dengan kategori yang belum ada di dalam array this.products yang akan ditambahkan ke dalam array
        if (!this.products.find((p) => p.category === data.category)) {
          this.products.push(data);
        }
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
