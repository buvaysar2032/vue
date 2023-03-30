<template>

  <li class="cart__item product" :key="item.productId">
    <div class="product__pic">
      <img :src="item.product.image" width="120" height="120" :alt="item.product.title">
    </div>
    <h3 class="product__title">
      {{ item.product.title }}
    </h3>
    <p class="product__info">
      Объем: <span>128GB</span>
    </p>
    <span class="product__code">
      Артикул: {{ item.product.id }}
    </span>

    <BaseCounter v-model.number="amount" :amount="amount"/>

    <b class="product__price">
      {{ (item.product.price * item.amount) | numberFormat }} ₽
    </b>

    <button class="product__del button-del" type="button" aria-label="Удалить товар из корзины" @click.prevent="deletProduct(item.productId)">
      <svg width="20" height="20" fill="currentColor">
        <use xlink:href="#icon-close"></use>
      </svg>
    </button>
  </li>

</template>

<script>
import BaseCounter from '@/components/BaseCounter.vue';
import numberFormat from '@/helpers/numberFormat';
import { mapActions } from 'vuex';

  export default {
    props: ['item'],
    components: {
      BaseCounter
    },
    filters: {
      numberFormat
    },
    computed: {
      amount: {
        get() {
          return this.item.amount
        },
        set(value) {
          this.$store.dispatch('updateCartProductAmount', {productId: this.item.productId, amount: value})
        }
      }
    },
    methods: {
      ...mapActions(["deleteProduct"]),
      deletProduct(productId) {
        this.deleteProduct(productId);
      }
    },
    watch: {
    amount() {
      if(!this.amount) {
        this.deletProduct(this.item.productId);
      }
    }
  },
  }
</script>
