<template>
  <div>
    <h3 v-if="products.length === 0">Liste yoxdur</h3>
    <table v-else>
      <thead>
        <tr>
          <th>Id</th>
          <th>UserId</th>
          <th>Title</th>
          <th>Changes</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td v-if="updateId === product.id">
            <input v-model="product.id" type="text" />
          </td>
          <td v-else>{{ product.id }}</td>
          <td v-if="updateId === product.id">
            <input v-model="product.userId" type="text" />
          </td>
          <td v-else>{{ product.userId }}</td>
          <td v-if="updateId === product.id">
            <input v-model="product.title" type="text" />
          </td>
          <td v-else>{{ product.title }}</td>
          <td v-if="updateId !== product.id">
            <button class="btn btn-primary" @click="handleUpdate(product)">
              Yenile
            </button>
            <button class="btn btn-danger" @click="handleClick(product)">
              Sil
            </button>
          </td>
          <td v-else>
            <button
              class="btn btn-primary"
              @click="handleUpdateProduct(product)"
            >
              Yadda saxla
            </button>
            <button class="btn btn-danger" @click="updateId = null">
              Geri
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "product-list",
  data() {
    return { updateId: null };
  },
  props: {
    products: Array,
  },

  methods: {
    handleUpdate(product) {
      this.updateId = product.id;
    },
    handleClick(product) {
      this.$emit("delete:product", product);
    },

    handleUpdateProduct(product) {
      this.$emit("update:product", product);
      this.updateId = null;
    },
  },
};
</script>

<style scoped>
table {
  width: 100%;
}
.btn {
  padding: 10px;
  border: none;
  outline: none;
  background: red;
  color: #fff;
  font-weight: 500;
  cursor: pointer;
}
.btn-primary {
  background-color: seagreen;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
