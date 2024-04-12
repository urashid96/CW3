<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button @click="showCheckout">
        {{ cartItemCount }}
        <span class="fas fa-cart-plus"></span> Checkout
      </button>
    </header>
    <main>
      <button @click="updateSorting('name')">Sort by Name</button>
      <button @click="updateSorting('price')">Sort by Price</button>
      <button @click="updateSorting('rating')">Sort by Rating</button>
      <product-list
        :products="sortedProducts"
        @add-to-cart="addToCart"
        v-if="showProduct"
      ></product-list>
      <checkout-component
        :cart="cart"
        :products="products"
        @remove-from-cart="removeFromCart"
        @back-to-lessons="backToLessons"
        v-else
      ></checkout-component>
    </main>
  </div>
</template>

<script>
import ProductList from './components/ProductList.vue'; // Import your ProductList
import checkoutcomponent from './components/checkoutcomponent.vue'; // Import your checkoutcomponent

export default {
  name: 'App',
  components: {
    ProductList,
    checkoutcomponent,
  },
  data() {
    return {
      sitename: 'Electronics Shop',
      showProduct: true,
      order: {
        firstName: '',
        lastName: '',
        address: '',
        city: '',
        zip: '',
        state: '',
        method: 'Home',
        gift: false,
        sendGift: 'Send as a gift',
        dontSendGift: 'Do not send as a gift',
        sortCriteria: 'name', // default sort criteria
        sortOrder: 'asc', // default sort order
      },
      states: {
        AD: 'Abu Dhabi',
        DU: 'Dubai',
        SH: 'Sharjah',
        AJ: 'Ajman',
        FU: 'Fujairah',
        RA: 'Ras Al Khaimah',
        UQ: 'Umm Al Quwain',
      },
      products: [],
      cart: [], // array to store items in shopping cart
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    addToCart(product) {
      this.cart.push(product.id);
    },
    fetchProducts() {
      // Fetch Products from the server
      fetch('http://localhost:3000/collection/products', {
        method: 'GET',
        headers: {
          'Content-Type': 'application/json',
        },
      })
        .then(response => response.json())
        .then(responseJSON => {
          // Update the Products data with the fetched Products
          this.products = responseJSON;
        })
        .catch(error => {
          console.error('Error fetching Products:', error);
        });
    },
    updateProduct(product) {
      // Assuming product is an object containing the updated product data
      fetch(`http://localhost:3000/collection/products/${product.id}`, {
        method: 'PUT',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(product),
      })
        .then(response => {
          if (!response.ok) {
            throw new Error('Failed to update product');
          }
          // Optionally handle success response here
        })
        .catch(error => {
          console.error('Error updating product:', error);
        });
    },
    addProduct(newProduct) {
      // Assuming newProduct is an object containing the data for the new product
      fetch('http://localhost:3000/collection/products', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(newProduct),
      })
        .then(response => {
          if (!response.ok) {
            throw new Error('Failed to add product');
          }
          // Optionally handle success response here
        })
        .catch(error => {
          console.error('Error adding product:', error);
        });
    },
    showCheckout() {
      this.showProduct = !this.showProduct;
    },
    submitForm() {
      event.preventDefault();
      alert('Order Submitted!');
    },
    canAddToCart(product) {
      return product.availableInventory > this.cartCount(product.id);
    },
    cartCount(id) {
      return this.cart.filter(productId => productId === id).length;
    },
    updateSorting(criteria) {
      if (this.order.sortCriteria === criteria) {
        // If the same criteria is clicked again, toggle the sort order
        this.order.sortOrder = this.order.sortOrder === 'asc' ? 'desc' : 'asc';
      } else {
        // If a new criteria is clicked, set it as the sort criteria and default to ascending order
        this.order.sortCriteria = criteria;
        this.order.sortOrder = 'asc';
      }
    },
    sortedProducts() {
      let productsArray = this.products.slice(0);
      const order = this.order;

      // Define a dynamic comparison function based on sortCriteria
      function compare(a, b) {
        if (a[order.sortCriteria] < b[order.sortCriteria]) return order.sortOrder === 'asc' ? -1 : 1;
        if (a[order.sortCriteria] > b[order.sortCriteria]) return order.sortOrder === 'asc' ? 1 : -1;
        return 0;
      }

      // Sort the products array using the dynamic comparison function
      return productsArray.sort(compare);
    },
    removeFromCart(productId) {
      const index = this.cart.indexOf(productId);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },
    backToLessons() {
      this.showProduct = true;
    },
  },
  computed: {
    cartItemCount() {
      return this.cart.length || '';
    },
  },
};
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(registration => {
        console.log('Service worker registered:', registration);
      })
      .catch(error => {
        console.error('Service worker registration failed:', error);
      });
  });
}

// Ensure that the app is installed as a PWA
if (window.matchMedia('(display-mode: standalone)').matches) {
  console.log('Display mode is standalone');
} else {
  console.log('Display mode is browser');
}
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
