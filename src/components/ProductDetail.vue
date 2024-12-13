<template>
  <br>
  <div class="product-detail" v-if="productExists">
    <div class="product-image">
      <img :src="product.image" :alt="product.name" />
    </div>
    <div class="product-info">
      <h2>{{ product.name }}</h2>
      <small>Product ID: {{ product.id }}</small>
      <p>{{ product.description }}</p>
      <div class="product-controls">
        <p>
          <b>Price: <span class="price">{{ product.price }}</span></b>
        </p>
        <input type="number" v-model="quantity" min="1" class="quantity-input" />
        <button @click="addToCart">Add to Cart</button>
      </div>
    </div>
  </div>
  <div class="product-detail" v-else>
    <img src="../assets/404.jpg" alt="Product not found" />
    <h3>Opps! That product was not found...</h3>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  props: ['products'],
  data() {
    return {
      quantity: 1
    }
  },
  computed: {
    product() {
      return this.products.find(product => product.id == this.$route.params.id);
    },
    productExists() {
      return !!this.product;
    }
  },
  methods: {
    addToCart() {
      // Add the product and quantity to the cart
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
a {
  color: #0071e3; /* Blue similar to Best Buy's accent color */
  text-decoration: none; /* Removing underline for cleaner look */
}

.product-detail {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 2rem;
  margin: 2rem 0;
  padding: 1rem;
  background-color: #f9f9f9; /* Light background for details */
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Soft shadow for depth */
}

.product-image {
  flex: 1;
  max-width: 500px;
  margin-right: 2rem;
}

.product-image img {
  width: 100%;
  height: auto;
  border-radius: 8px; /* Rounded image corners */
}

.product-info {
  flex: 2;
  max-width: 600px;
}

.product-info h2 {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
}

.product-info small {
  display: block;
  font-size: 14px;
  color: #999;
  margin-bottom: 10px;
}

.product-info p {
  font-size: 16px;
  margin-bottom: 20px;
  color: #555;
}

.product-controls {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.product-controls p {
  font-size: 18px;
  font-weight: bold;
}

.product-controls .price {
  color: #ff6a00; /* Price color similar to Best Buy's */
  font-size: 20px;
}

.product-controls input {
  width: 60px;
  padding: 5px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
  text-align: center;
}

.product-controls button {
  padding: 10px 20px;
  background-color: #ff6a00;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.product-controls button:hover {
  background-color: #e05a00; /* Darker shade on hover */
}

@media (max-width: 768px) {
  .product-detail {
    flex-direction: column;
  }
  .product-image {
    margin-right: 0;
    margin-bottom: 1rem;
  }
}
</style>
