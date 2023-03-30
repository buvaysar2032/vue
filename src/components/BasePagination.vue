<template>
  <ul class="catalog__pagination pagination" v-if="pages > 1">
    <li class="pagination__item">
      <button class="pagination__link pagination__link--arrow" :disabled="page === 1" @click.prevent="prevPage(page)" aria-label="Предыдущая страница">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-left"></use>
        </svg>
      </button>
    </li>
    <li class="pagination__item" v-for="pageNumber of pages" :key="pageNumber">
      <a href="#" class="pagination__link" :class="{'pagination__link--current' : pageNumber === page}" @click.prevent="paginate(pageNumber)">
        {{ pageNumber }}
      </a>
    </li>
    <li class="pagination__item">
      <button class="pagination__link pagination__link--arrow" :disabled="page === pages" @click.prevent="nextPage(page)" aria-label="Следующая страница">
        <svg width="8" height="14" fill="currentColor">
          <use xlink:href="#icon-arrow-right"></use>
        </svg>
      </button>
    </li>
  </ul>
</template>

<script>
  export default {
    model: {
      prop: 'page',
      event: 'paginate'
    },
    props: ['page', 'count', 'perPage'],
    computed: {
      pages() {
        return Math.ceil(this.count / this.perPage)
      }
    },
    methods: {
      paginate(page) {
        this.$emit('paginate', page)
      },
      prevPage(page) {
        if(page > 1) {
          this.$emit('paginate', page - 1)
        }
      },
      nextPage(page) {
        if(page < this.pages) {
          this.$emit('paginate', page + 1)
        }
      },
    }
  }
</script>
