<template>
  <div class="cart-container">
    <!-- IF NO PRODUCTS IN CART, DISPLAY ALERT -->
    <div v-if="items.length === 0" class="item-container-message">
      No Products Added!
    </div>
    <div v-for="(item, i) in items" :key="i" class="item-container">
      <!-- IMG -->
      <div class="cart-img-container">
        <img :src="require(`@/assets/${item.image}`)" alt="some pic" />
      </div>
      <!-- TITLE -->
      <div class="cart-title">{{ item.title }}</div>
      <!-- SIZE -->
      <div class="size-detail">Size: {{ item.size }}</div>
      <!-- QUANTITY -->
      <div class="qty-detail">
        <div class="qty-decrement" @click="decrement(i)">
          <i class="fas fa-minus-circle"></i>
        </div>
        <div class="qty-count" v-if="item.qty">{{ item.qty }}</div>
        <div class="qty-increment" @click="increment(i)">
          <i class="fas fa-plus-circle"></i>
        </div>
        <!-- TOTAL PRICE -->
        <div class="total-price">{{ item.qty * item.price }} $</div>
      </div>
      <!-- REMOVE BTN -->
      <div class="remove-btn" @click="removeProduct(i)">
        <i class="fas fa-trash"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CartDetail',
  props: {
    items: Array,
  },
  methods: {
    increment(i) {
      this.$emit('increment', i)
    },
    decrement(i) {
      this.$emit('decrement', i)
    },
    removeProduct(i) {
      this.$emit('removeProduct', i)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cart-container {
  width: 500px;
  padding: 5px;
  background-color: #ebebeb;
}
.item-container {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr 2fr 1fr auto;
  align-items: center;
  border: 1px solid transparent;
  border-bottom-color: #ddd;
}

.item-container-message {
  text-align: center;
  padding: 20px;
  color: #000;
}
.qty-detail {
  display: flex;
  justify-content: space-evenly;
}

.qty-increment,
.qty-decrement {
  cursor: pointer;
}

.cart-img-container {
  padding: 3px;
  width: 70px;
  height: 70px;
  object-fit: contain;
}
img {
  width: 100%;
  height: 100%;
}

.remove-btn {
  color: #ef1c27;
  text-align: center;
  cursor: pointer;
}
</style>
