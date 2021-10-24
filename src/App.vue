<template>
  <div id="app">
    <Header :cartItems="cartItems" :itemCount="itemCount" />
    <!-- SHOPPING CART ITEMS DISPLAYED ON ICON HOVER -->
    <div class="fake-cart">
      <div class="fake-icon-container"></div>
      <div class="animated-cart">
        <CartDetail
          :items="cartItems"
          @increment="increment"
          @decrement="decrement"
          @removeProduct="removeProduct"
        />
      </div>
    </div>
    <!-- ALERT WHEN PRODUCT ADDED -->
    <div v-if="displayAlert" class="alert-message">
      Added to the Bag
    </div>
    <div class="container">
      <div class="row">
        <div class="col" v-for="product in productList" :key="product.id">
          <ProductCard :product="product" @addToCart="addToCart($event)" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import ProductCard from './components/ProductCard.vue'
import CartDetail from './components/CartDetail.vue'
import data from './data.json'

export default {
  name: 'App',
  components: {
    Header,
    ProductCard,
    CartDetail,
  },
  data() {
    return {
      productList: data,
      cartItems: [],
      displayAlert: false,
    }
  },
  computed: {
    itemCount: function() {
      console.log(this.cartItems.reduce((acc, c) => acc + c.qty, 0))
      return this.cartItems.reduce((acc, c) => acc + c.qty, 0)
    },
  },
  methods: {
    // add product
    addToCart(val) {
      // display alert 1.5 seconds
      this.displayAlert = true
      setTimeout(() => {
        this.displayAlert = false
      }, 1500)
      setTimeout
      // filter products with the same IDs.
      const sameProducts = this.cartItems.filter(
        (product) => product.id === val.id
      )
      // filter same id products with same sizes
      const sameSizes = sameProducts.filter(
        (product) => product.size === val.size
      )
      // if there is no same products, add it to the cart
      if (sameProducts.length === 0) {
        this.cartItems.push({ cartId: new Date().getTime(), ...val })
      }
      // if the same size and id available, increase  qty
      else if (sameSizes.length > 0) {
        const targetIndex = this.cartItems.findIndex(
          (el) => el.id === val.id && el.size === val.size
        )
        this.cartItems[targetIndex].qty += val.qty
      }
      // if size is not the same, add it to the cart
      else {
        this.cartItems.push({ cartId: new Date().getTime(), ...val })
      }
    },
    increment(i) {
      this.cartItems[i].qty += 1
    },
    decrement(i) {
      // if there is only one item, remove it
      if (this.cartItems[i].qty === 1) {
        this.removeProduct(i)
      } else {
        this.cartItems[i].qty -= 1
      }
    },
    removeProduct(i) {
      this.cartItems.splice(i, 1)
    },
  },
}
</script>

<style>
#app {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.fake-cart {
  position: absolute;
  display: block;
  background-color: transparent;
  right: 60px;
  top: 13px;
  width: 40px;
  height: 40px;
  padding-bottom: 50px;
}

.animated-cart {
  z-index: 999;
  position: absolute;
  top: 51px;
  right: -560px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 3px;

  transition: right 1s ease;
}
.fake-icon-container {
  width: 40px;
  height: 40px;
  position: absolute;
  top: 0;
  right: 0;
  cursor: pointer;
}

.fake-cart:hover .fake-icon-container {
  background-color: grey;
  border-radius: 100%;
  opacity: 0.1;
}

.fake-cart:hover .animated-cart {
  right: -60px;
}
.alert-message {
  position: absolute;
  background-color: #000;
  -webkit-font-smoothing: antialiased;
  color: #fff;
  border-radius: 3px;
  top: 60px;
  right: 10px;
  padding: 10px 20px;
  display: inline-block;
}
.container {
  margin: 10px;
  padding: 0;
}
.row {
  display: flex;
  flex-wrap: wrap;
  padding: 0;
}
</style>
