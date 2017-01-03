<template>
  <div id='searchbox-template'>
    <input type='text' placeholder='Search...' v-model='searchText' />
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
          <th>Category</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for='p in filteredProducts'>
          <td :class='{ soldout: !p.stocked }'>{{ p.name }}</td>
          <td>{{ p.price }}</td>
          <td>{{ p.category }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.soldout {
  color: red;
}
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
      searchText: ''
    }
  },
  computed: {
    filteredProducts: function() {
      return this.products.filter((p) => {
        return p.name.indexOf(this.searchText) !== -1 || p.price.indexOf(this.searchText) !== -1 ||
          p.category.indexOf(this.searchText) !== -1;
      });
    },
  },
}
</script>
