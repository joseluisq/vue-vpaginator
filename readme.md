# vue-vpaginator

> [Vue.js 2](https://vuejs.org/) + [Bootstrap]() paginator component for [Laravel Pagination](https://laravel.com/docs/5.4/pagination) response data.

![vpagination](https://cloud.githubusercontent.com/assets/1700322/23525455/e556a020-ff8e-11e6-9c38-78fb5ef85aa9.png)

## Install

```sh
npm install vue-vpaginator --save-dev
```

## Prerequisites

- [Vue.js 2](https://vuejs.org/)
- [jQuery](https://github.com/jquery/jquery)
- [jQuery BootPag](https://github.com/botmonster/jquery-bootpag)
- Some [Laravel Pagination](https://laravel.com/docs/5.4/pagination) result

## Usage

In your custom component:

`my-custom-component.vue`

```html
<template>
    <table class="table">
      ...
    </table>

    <vpaginator :response="myResponseData" @paginate="fetchMyServerData"></vpaginator>
</template>

<script>
  export default {
    data () {
      return {
        myResponseData: {}
      }
    },

    mounted () {
      this.fetchMyServerData()
    },

    methods: {
      /**
       * Fetch my data from server
       */
      fetchMyServerData (page = 1) {
        // Fetching some data from server...
        axios.get(`/api/v1/product/?page=${page}`)
          .then(response => response.data)
          .then(response => {
            // Setting the response data (Laravel Pagination data)
            this.myResponseData = response
            // ...
          })
      }
    }
  }
</script>
```

In your entry app:

```js
const Vue = require('vue')

// jQuery
window.$ = window.jQuery = require('jquery')

// jQuery BootPag
// require using a path because it has not some main entry file
require('bootpag/lib/jquery.bootpag')

// require vpaginator
Vue.component('vpaginator', require('vue-vpaginator'))

// require your custom component
Vue.component('my-custom-component', require('./components/my-custom-component'))

const app = new Vue({
  el: '#app'
})
```

_Make sure that your Laravel app returns a [Pagination](https://laravel.com/docs/5.4/pagination) data._

## Attributes

#### response
The response `data` name for store the [Laravel Pagination](https://laravel.com/docs/5.4/pagination) data. E.g. `v-bind:response="myResponseData"` or `:response="myResponseData"`.

## Events

#### @paginate (page)

It fires when some `page` number is clicked. You need to pass a callback (`method: ...`).

## License
MIT license

© 2017 [José Luis Quintana](http://git.io/joseluisq)
