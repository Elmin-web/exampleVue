<template>
  <div id="app">
    <AddProduct @add:product="addProduct" />
    <ProductList
      @delete:product="deleteProduct"
      @update:product="updateProduct"
      :products="products"
    />
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import AddProduct from "./components/AddProduct.vue";

export default {
  name: "App",
  components: {
    ProductList,
    AddProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.getProducts();
  },

  methods: {
    async getProducts() {
      const result = await fetch("http://localhost:3000/example");
      const res = await result.json();
      this.products = res;
    },
    async updateProduct(product) {
      const result = await fetch(
        "http://localhost:3000/example/" + product.id,
        {
          method: "PUT",
          body: JSON.stringify(product),
          headers: { "Content-Type": "application/json" },
        }
      );
      const updatedProduct = await result.json();
      this.products = this.products.map((product) =>
        product.id === updatedProduct.id ? updatedProduct : product
      );
    },
    async deleteProduct(product) {
      if (confirm("eminsiz?")) {
        let obj = {
          method: "DELETE",
        };
        await fetch("http://localhost:3000/example/" + product.id, obj);
        this.products = this.products.filter(
          (filterProduct) => filterProduct.id !== product.id
        );
      }
    },
    async addProduct(product) {
      const result = await fetch("http://localhost:3000/example", {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type": "application/json" },
      });
      const newProduct = await result.json();
      this.products = [...this.products, newProduct];
      alert("Product Added");
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
