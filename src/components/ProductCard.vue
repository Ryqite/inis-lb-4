<script>
import cartIcon from '../assets/cart.svg'
import starIcon from '../assets/star.svg'

export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  emits: ['add-to-cart'],
  data() {
    return {
      maxRating: 5,
      cartIcon,
      starIcon,
    }
  },
  computed: {
    stars() {
      return Array.from({ length: this.maxRating }, (_, i) => i < Math.round(this.product.rating))
    },
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.product)
    },
  },
}
</script>

<template>
  <article class="card">
    <img class="image" :src="product.image" :alt="product.name" />
    <h3 class="title">{{ product.name }}</h3>
    <p class="category">{{ product.category }}</p>

    <div class="rating" :aria-label="`Рейтинг ${product.rating} из ${maxRating}`">
      <img
        v-for="(filled, index) in stars"
        :key="index"
        :src="starIcon"
        alt=""
        :class="filled ? 'star-filled' : 'star-empty'"
      />
    </div>

    <p class="price">${{ product.price.toFixed(2) }}</p>

    <button type="button" class="button" @click="addToCart">
      <img class="button-icon" :src="cartIcon" alt="" />
      Добавить в корзину
    </button>
  </article>
</template>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  gap: 12px;
  width: 320px;
  padding: 16px;
  background: var(--neutral-0);
  border: 1px solid transparent;
  border-radius: var(--radius-card);
  box-shadow: var(--shadow-card);
  transition: box-shadow 0.2s, border-color 0.2s;
}
.card:hover {
  border-color: var(--brand-primary);
  box-shadow: var(--shadow-card-hover);
}

.image {
  width: 288px;
  height: 216px;
  object-fit: cover;
  border-radius: var(--radius-control);
}

.title {
  margin: 0;
  font-size: 16px;
  line-height: 24px;
  font-weight: 600;
}

.category {
  margin: 0;
  font-size: 14px;
  line-height: 20px;
  color: var(--neutral-600);
}

.rating {
  display: flex;
  gap: 2px;
}
.star-filled,
.star-empty {
  width: 16px;
  height: 16px;
}
.star-empty {
  opacity: 0.2;
}
.star-filled {
  filter: invert(68%) sepia(80%) saturate(2000%) hue-rotate(10deg);
}

.price {
  margin: 0;
  font-size: 24px;
  line-height: 32px;
  font-weight: 700;
}

.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 12px 24px;
  border: 2px solid transparent;
  border-radius: var(--radius-control);
  background: var(--brand-primary);
  color: var(--neutral-0);
  font: 600 16px/24px 'Inter', sans-serif;
  cursor: pointer;
  transition: background-color 0.2s;
}
.button:hover {
  background: var(--brand-primary-hover);
}
.button:active {
  background: var(--brand-primary-pressed);
}
.button-icon {
  width: 20px;
  height: 20px;
  filter: brightness(0) invert(1);
}
</style>
