<script>
export default {
  name: 'ShoppingCart',
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  emits: ['remove'],
  computed: {
    total() {
      return this.items.reduce((sum, item) => sum + item.price * item.quantity, 0)
    },
  },
}
</script>

<template>
  <aside class="cart">
    <h2 class="heading">Корзина</h2>

    <p v-if="items.length === 0" class="empty">Корзина пуста</p>

    <template v-else>
      <ul class="list">
        <li v-for="item in items" :key="item.id" class="item">
          <div class="info">
            <span class="name">{{ item.name }}</span>
            <span class="details">{{ item.quantity }} × ${{ item.price.toFixed(2) }}</span>
          </div>
          <button
            type="button"
            class="remove"
            :aria-label="`Удалить ${item.name}`"
            @click="$emit('remove', item.id)"
          >
            ×
          </button>
        </li>
      </ul>

      <p class="total">
        <span>Итого</span>
        <strong>${{ total.toFixed(2) }}</strong>
      </p>
    </template>
  </aside>
</template>

<style scoped>
.cart {
  width: 320px;
  padding: 16px;
  background: var(--neutral-0);
  border-radius: var(--radius-card);
  box-shadow: var(--shadow-card);
}

.heading {
  margin: 0 0 16px;
  font-size: 24px;
  line-height: 32px;
  font-weight: 700;
}

.empty {
  margin: 0;
  color: var(--neutral-600);
}

.list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 12px 0;
  border-bottom: 1px solid var(--neutral-100);
}

.info {
  display: flex;
  flex-direction: column;
}
.name {
  font-weight: 600;
}
.details {
  font-size: 14px;
  color: var(--neutral-600);
}

.remove {
  width: 32px;
  height: 32px;
  border: none;
  border-radius: var(--radius-control);
  background: transparent;
  color: var(--state-danger);
  font-size: 20px;
  line-height: 1;
  cursor: pointer;
}
.remove:hover {
  background: var(--neutral-100);
}

.total {
  display: flex;
  justify-content: space-between;
  margin: 16px 0 0;
  font-size: 20px;
  line-height: 28px;
}
</style>
