<template>
  <div class="nav-header">
    <nav type="dark" class="px-5">
      <div href="#" title="Don't do it">
        <img src="../assets/mike-logo.jpeg" alt="mike-logo" />
      </div>
      <div class="cart-wrapper">
        <div class="cart-icon-container">
          <b-icon icon="bag" class="cart-icon" />

          <div class="product-count">{{ itemCount }}0</div>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    itemCount: Number,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.nav-header {
  width: 100vw;
  border-bottom: 1px solid #ebebeb;
  padding: 10px;
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

img {
  width: 70px;
  border-radius: 3px;
}

.cart-wrapper {
  background-color: transparent;
  padding: 10px;
  border-radius: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 100%;
}

.cart-wrapper:hover {
  background-color: #ebebeb;
}
.cart-icon-container {
  position: relative;
  display: flex;
  align-items: center;
}

.product-count {
  font-size: 11px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 3px;
  color: #000;
  font-weight: 600;
  width: 24px;
  height: 24px;
}
.cart-icon {
  color: #000;
  font-size: 24px;
}
</style>
