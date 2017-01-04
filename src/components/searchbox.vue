<template lang='jade'>
  #searchbox-template
    input(type='text' placeholder='Search...' v-model='searchText')
    p
      input(type='checkbox' id='stock' v-model='stocked')
      label(for='stock')= ' Only show products in stock'
    table
      thead
        tr
          th Name
          th Price
          th Category
      tbody
        tr(v-for='p in filteredProducts')
          td(:class='{ soldout: !p.stocked }') {{ p.name }}
          td {{ p.price }}
          td {{ p.category }}
</template>

<style lang='stylus' scoped>
.soldout
  color red
</style>

<script>
export default {
  name: 'searchbox-template',

  data() {
    return {
      products: [
        {category: 'Sproting Goods', price: '$49.99', stocked: true, name: 'Football'},
        {category: 'Sproting Goods', price: '$9.99', stocked: true, name: 'Baseball'},
        {category: 'Sproting Goods', price: '$29.99', stocked: false, name: 'Basketball'},
        {category: 'Electornics', price: '$99.99', stocked: true, name: 'iPod Touch'},
        {category: 'Electornics', price: '$399.99', stocked: false, name: 'iPhone 5'},
        {category: 'Electornics', price: '$199.99', stocked: true, name: 'Nexus 7'},
      ],
      searchText: '',
      stocked: false
    }
  },

  computed: {
    filteredProducts: function() {
      return this.products.filter(p => {
        const isStocked = this.stocked ? p.stocked === true : true
        const isName = p.name.indexOf(this.searchText) !== -1;
        const isPrice = p.price.indexOf(this.searchText) !== -1;
        const isCategory = p.category.indexOf(this.searchText) !== -1;
        return isStocked && (isName || isPrice || isCategory);
      });
    },
  },
}
</script>
