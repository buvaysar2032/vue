<template>
  <main class="content container">
    <div class="content__top">
      <ul class="breadcrumbs">
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link" href="index.html">
            Каталог
          </a>
        </li>
        <li class="breadcrumbs__item">
          <a class="breadcrumbs__link">
            Корзина
          </a>
        </li>
      </ul>

      <h1 class="content__title">
        Корзина
      </h1>
      <span v-if="!$store.state.cartProductsData.length" class="content__info">Корзина пуста</span>
      <span v-else class="content__info">
        {{
          $store.state.cartProductsData.reduce((res, item) => item.quantity + res, 0)
        }}
        товара
      </span>
    </div>

    <section class="cart">
      <form class="cart__form form" action="#" method="POST">
        <div class="cart__field">
          <ul class="cart__list">
            <CartItem v-for="item in products" :key="item.productId" :item="item"/>
          </ul>
        </div>

        <div class="cart__block" v-if="$store.state.cartProductsData.length">
          <p class="cart__desc">
            Мы&nbsp;посчитаем стоимость доставки на&nbsp;следующем этапе
          </p>
          <p class="cart__price">
            Итого: <span>{{ totlaPrice | numberFormat }} ₽</span>
          </p>

          <button class="cart__button button button--primery" type="submit">
            Оформить заказ
          </button>
        </div>
      </form>
    </section>
  </main>
</template>

<script>
  import { mapGetters } from 'vuex';
  import CartItem from '@/components/CartItem.vue';
  import numberFormat from '@/helpers/numberFormat';
  export default {
    components: {
    CartItem
    },
    computed: {
      ...mapGetters({products: 'cartDetailProducts', totlaPrice: 'cartTotalPrice'}),
    },
    filters: {numberFormat}
  }
</script>
