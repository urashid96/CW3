<template>
  <div class="checkout-form">
    <h2>Checkout</h2>
    <div class="cart-items">
      <h2>Cart Items</h2>
      <div v-if="cart.length === 0">
        <p>Your cart is empty.</p>
      </div>
      <div v-else>
        <div v-for="cartItem in cart" :key="cartItem.id" class="cart-item">
          <h3>{{ getProductById(cartItem.id).title }}</h3>
          <figure>
            <img :src="getProductById(cartItem.id).image" alt="Product Image">
          </figure>
          <p v-html="getProductById(cartItem.id).description"></p>
          <p>Price: {{ getProductById(cartItem.id).price }}</p>
          <!-- Assuming location and spaces are properties of the product -->
          <p>Location: {{ getProductById(cartItem.id).location }}</p>
          <p>Spaces: {{ cartItem.quantity }}</p>
          <button @click="removeFromCart(cartItem.id)">Remove</button>
        </div>
      </div>
    </div>
    <button @click="$emit('back-to-lessons')">Back to Lessons</button>
  </div>
</template>

<script>
export default {
  name: 'checkout-component',
  props: {
    cart: Array,
    products: Array,
  },
  methods: {
    removeFromCart(productId) {
      this.$emit('remove-from-cart', productId);
    },
    getProductById(productId) {
      const product = this.products.find(p => p.id === productId);
      if (!product) {
        console.error(`Product with ID ${productId} not found.`);
        return {};
      }
      return product;
    },
  },
};
</script>

<style scoped>
/* Add scoped styles here */
.checkout-form {
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin: 20px 0;
}

.cart-items {
  margin-top: 20px;
}

.cart-item {
  border: 1px solid #ccc;
  padding: 10px;
  margin-bottom: 10px;
}
</style>


<style scoped>
/* Include the styles from styles.css */
.checkout-form {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  border: 3px solid #ccc;
  border-radius: 10px;
  background-color: #f9f9f9;
}

.checkout-form h2 {
  margin-top: 0;
}

.checkout-form p {
  margin-bottom: 10px;
}

.checkout-form .cart-items {
  margin-top: 20px;
}

.checkout-form .cart-item {
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 5px;
}

.checkout-form .cart-item h3 {
  margin-top: 0;
}

.checkout-form .cart-item figure {
  margin-bottom: 10px;
}

.checkout-form .cart-item img {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 5px;
}

.checkout-form .cart-item p {
  margin: 5px 0;
}

.checkout-form .cart-item button {
  background-color: #f44336;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 3px;
  cursor: pointer;
}

.checkout-form .cart-item button:hover {
  background-color: #d32f2f;
}

.checkout-form button {
  background-color: #333;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 20px;
}

.checkout-form button:hover {
  background-color: #1ea5da;
}
</style>
