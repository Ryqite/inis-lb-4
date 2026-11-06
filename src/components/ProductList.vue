<script>
import ProductCard from './ProductCard.vue'

export default {
  name: 'ProductList',
  components: { ProductCard },
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  emits: ['add-to-cart'],
  data() {
    return {
      searchQuery: '',
    }
  },
  computed: {
    filteredProducts() {
      const query = this.searchQuery.trim().toLowerCase()
      return this.products.filter((product) => product.name.toLowerCase().includes(query))
    },
  },
}
</script>

<template>
  <section>
    <h2 class="heading">Каталог</h2>

    <input
      v-model="searchQuery"
      class="search"
      type="search"
      placeholder="Поиск по названию"
      aria-label="Поиск по названию"
    />

    <div v-if="filteredProducts.length" class="grid">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @add-to-cart="$emit('add-to-cart', $event)"
      />
    </div>
    <p v-else class="empty">Ничего не найдено</p>
  </section>
</template>

<style scoped>
.heading {
  margin: 0 0 16px;
  font-size: 24px;
  line-height: 32px;
  font-weight: 700;
}

.search {
  width: 100%;
  max-width: 400px;
  margin-bottom: 24px;
  padding: 10px 14px;
  border: 1px solid var(--neutral-300);
  border-radius: var(--radius-control);
  background: var(--neutral-0);
  font: 400 16px/24px 'Inter', sans-serif;
}
.search:focus {
  outline: 2px solid var(--brand-primary);
  outline-offset: 1px;
}

.grid {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

.empty {
  color: var(--neutral-600);
}
</style>
