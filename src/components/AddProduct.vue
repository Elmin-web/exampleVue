<template>
  <div>
    <form @submit.prevent="addProduct()">
      <div>
        <label for="productId">productId</label>
        <input v-model="product.userId" type="text" name="productId" />
        <label for="productName">productName</label>
        <input type="text" v-model="product.title" name="productName" />
        <label for="productPrice">productPrice</label>
        <input v-model="product.completed" type="text" name="productPrice" />
        <button type="submit">Artir</button>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  name: "addproduct",
  data() {
    return {
      product: {
        id: "",
        userId: "",
        title: "",
        completed: "",
      },
    };
  },
  methods: {
    addProduct() {
      this.$emit("add:product", this.product);
    },
  },
};
</script>
<style scoped>
form {
  width: 60%;
  margin: 0 auto;
}
input {
  width: 100%;
  outline: none;
}
button {
  padding: 20px;
  background-color: greenyellow;
  color: #000;
}
</style>
