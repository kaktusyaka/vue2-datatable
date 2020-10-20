<template>
  <nav class="pagination relative z-0 inline-flex shadow-sm" name="Pagination">
    <a href="#" class="page-link relative inline-flex items-center px-2 py-2 rounded-l-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-500 hover:text-gray-400 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" v-if="!isFirstPage" @click="turnPage(-1)" @click.prevent>
      <svg class="h-5 w-5" x-description="Heroicon name: chevron-left" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd"></path>
      </svg>
    </a>
    <a v-if="i" v-for="i in dspBtns" href="#" class="page-link -ml-px relative inline-flex items-center px-4 py-2 border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-700 hover:text-gray-500 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150" @click.prevent="handleClick(i)">
      {{ i }}
    </a>
    <a href="#" v-if="!isLastPage" @click="turnPage(1)" class="page-link -ml-px relative inline-flex items-center px-2 py-2 rounded-r-md border border-gray-300 bg-white text-sm leading-5 font-medium text-gray-500 hover:text-gray-400 focus:z-10 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue active:bg-gray-100 active:text-gray-500 transition ease-in-out duration-150" @click.prevent>
      <svg class="h-5 w-5" x-description="Heroicon name: chevron-right" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"></path>
      </svg>
    </a>
  </nav>
</template>
<script>
export default {
  name: 'Pagination',
  props: {
    total: { type: Number, required: true },
    query: { type: Object, required: true }
  },
  computed: {
    isFirstPage () {
      return +this.query.offset === 0 || +this.query.limit >= this.total
    },
    isLastPage () {
      return +this.query.offset + +this.query.limit >= this.total
    },
    totalPage () {
      return Math.ceil(this.total / +this.query.limit)
    },
    curPage () {
      return Math.ceil(+this.query.offset / +this.query.limit) + 1
    },
    dspBtns () {
      const n = this.totalPage
      const i = this.curPage

      /* eslint-disable */
      if (n <= 9) return ((n) => {
        const arr = Array(n)
        while (n) { arr[n - 1] = n-- }
        return arr
      })(n)
      if (i <= 5) return [1, 2, 3, 4, 5, 6, 7, 0, n] // 0 represents `···`
      if (i >= n - 4) return [1, 0, n-6, n-5, n-4, n-3, n-2, n-1, n]
      return [1, 0, i-2, i-1, i, i+1, i+2, 0, n]
      /* eslint-enable */
    }
  },
  methods: {
    handleClick (n) {
      this.query.offset = (n - 1) * +this.query.limit
    },
    turnPage (i) {
      if (i < 0 && this.isFirstPage || i > 0 && this.isLastPage) return
      this.query.offset = +this.query.offset + i * +this.query.limit
    }
  }
}
</script>
