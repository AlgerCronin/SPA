# SPA
// Define routes
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  { path: '/contact', component: Contact },
  { path: '/products', component: Products },
  { path: '/products/:id', component: ProductDetails },
  { path: '*', component: NotFound }
];

// Create router instance
const router = new VueRouter({
  routes
});

// Create Vue instance
new Vue({
  el: '#app',
  router,
  data() {
    return {
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter(item => item.id !== productId);
    }
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price, 0);
    }
  },
  template: `
    <div>
      <header>
        <!-- Navigation -->
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
        <router-link to="/contact">Contact</router-link>
        <router-link to="/products">Products</router-link>
        <router-link to="/cart">Cart</router-link>
      </header>
      <main>
        <!-- Router view -->
        <router-view></router-view>
        <!-- Shopping cart -->
        <div v-if="$route.path === '/cart'">
          <h2>Shopping Cart</h2>
          <ul>
            <li v-for="item in cart" :key="item.id">
              {{ item.name }} - {{ item.price }}
              <button @click="removeFromCart(item.id)">Remove</button>
            </li>
          </ul>
          <p>Total: {{ totalPrice }}</p>
        </div>
      </main>
      <footer>
        <!-- Footer -->
      </footer>
    </div>
  `
});
