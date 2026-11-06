# SampleShop — Vue (ЛР, вариант 3)

Интернет-магазин цифровых товаров на Vue 3 (Options API): `ProductCard.vue`, `ProductList.vue`,
`ShoppingCart.vue`. Данные передаются через props, события — через `$emit`, корзина (`cartItems`)
хранится в родительском компоненте `App.vue`.

## Запуск

Требуется Node.js 20+.

```bash
npm install
npm run dev
```

Откройте адрес, который выведет Vite (по умолчанию http://localhost:5173). Сборка: `npm run build`.

## Структура

```
src/
  assets/                  SVG-иконки, изображения товаров, main.css (переменные)
  data/products.js         mock-данные товаров
  components/
    ProductCard.vue        карточка товара, $emit('add-to-cart')
    ProductList.vue        список карточек, поиск (v-model), v-for, v-if / v-else
    ShoppingCart.vue       содержимое корзины, $emit('remove')
  App.vue                  cartItems, добавление и удаление товаров
```
