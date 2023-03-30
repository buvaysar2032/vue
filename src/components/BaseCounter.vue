<template>
  <div class="form__counter">
    <button type="button" aria-label="Убрать один товар" @click.prevent="minus(amount)">
      <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-minus"></use>
      </svg>
    </button>

    <input type="text" v-model.number="amount">

    <button type="button" aria-label="Добавить один товар" @click.prevent="plus(amount)">
      <svg width="12" height="12" fill="currentColor">
        <use xlink:href="#icon-plus"></use>
      </svg>
    </button>
  </div>
</template>

<script>
  export default {
    model: {
      prop: 'amount',
      event: 'increment'
    },
    props: ['amount'],

    methods: {
      plus(amount) {
        this.$emit('increment', amount + 1)
      },
      minus(amount) {
        if(amount <= 1) {
          amount = 1
        } else {
        this.$emit('increment', amount -1)
        }
      }
    },
  }
</script>
