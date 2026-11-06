<script>
import ProductList from './components/ProductList.vue'
import ShoppingCart from './components/ShoppingCart.vue'
import cartIcon from './assets/cart.svg'
import { products } from './data/products.js'

export default {
  name: 'App',
  components: { ProductList, ShoppingCart },
  data() {
    return {
      products,
      cartItems: [],
      cartIcon,
    }
  },
  computed: {
    cartCount() {
      return this.cartItems.reduce((sum, item) => sum + item.quantity, 0)
    },
  },
  methods: {
    addToCart(product) {
      const existing = this.cartItems.find((item) => item.id === product.id)
      if (existing) {
        existing.quantity += 1
      } else {
        this.cartItems.push({ id: product.id, name: product.name, price: product.price, quantity: 1 })
      }
    },
    removeFromCart(id) {
      this.cartItems = this.cartItems.filter((item) => item.id !== id)
    },
  },
}
</script>

<template>
  <div class="page">
    <header class="header">
      <h1 class="logo">SampleShop</h1>
      <div class="cart-icon">
        <img :src="cartIcon" alt="Корзина" />
        <span v-if="cartCount > 0" class="badge">{{ cartCount }}</span>
      </div>
    </header>

    <main class="layout">
      <ProductList :products="products" @add-to-cart="addToCart" />
      <ShoppingCart :items="cartItems" @remove="removeFromCart" />
    </main>
  </div>
</template>

<style scoped>
.page {
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 32px 48px;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24px 0;
}

.logo {
  margin: 0;
  font-size: 32px;
  line-height: 40px;
  font-weight: 700;
  color: var(--brand-primary);
}

.cart-icon {
  position: relative;
}
.cart-icon img {
  width: 32px;
  height: 32px;
}
.badge {
  position: absolute;
  top: -8px;
  right: -10px;
  min-width: 20px;
  padding: 0 6px;
  border-radius: 10px;
  background: var(--state-danger);
  color: var(--neutral-0);
  font-size: 10px;
  line-height: 20px;
  font-weight: 600;
  text-align: center;
}

.layout {
  display: flex;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 32px;
}
.layout > :first-child {
  flex: 1;
  min-width: 320px;
}
</style>
