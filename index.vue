<template>
  <div></div>
</template>

<script>
export default {
  props: {
    /**
     * "response" prop should have the same structure of
     * Laravel Pagination result https://laravel.com/docs/5.4/pagination
     */
    'response': {
      type: Object,
      default: () => {
        return {
          total: 1,
          per_page: 1,
          current_page: 1,
          last_page: 1,
          next_page_url: null,
          prev_page_url: null,
          from: 1,
          to: 1,
          data: []
        }
      }
    }
  },

  watch: {
    'response': function (response) {
      this.$bp.bootpag(this.getOptions(response))
    }
  },

  mounted () {
    this.$bp = $(this.$el)
    this.$bp.bootpag(this.getOptions(this.response))
      .on('page', (event, page) => {
        this.current_page = page
        this.$emit('paginate', page)
      })
  },

  methods: {
    getOptions (res) {
      return {
        total: res.per_page > res.total ? 1 : Math.round(res.total / res.per_page),
        page: res.current_page,
        maxVisible: res.total
      }
    }
  }
}
</script>
