<template>
  <div class="product-card" :class="product.color">
    <!-- LEFT -->
    <div class="left">
      <!-- PRODUCT IMG -->
      <div class="img-container">
        <img
          :src="require(`@/assets/${product.images[selectedImgIndex]}`)"
          alt="pink"
          class="img"
        />
      </div>
      <!-- OTHER IMGS -->
      <div class="img-preview-container">
        <div
          class="preview"
          v-for="(link, i) in product.images"
          :key="i"
          @click="changeImage(i)"
        >
          <img
            :src="require(`@/assets/${link}`)"
            :alt="`${product.title}-${i + 1}`"
            class="thumbnail"
          />
        </div>
      </div>
    </div>
    <!-- RIGHT -->
    <div class="right">
      <h3>{{ product.title }}</h3>
      <!-- AVAILABLE SIZES -->
      <ul class="sizes-container">
        <li
          v-for="(sizeData, i) in product.sizes"
          :key="sizeData.size"
          :class="{
            'sold-out': !sizeData.inStock,
            selected: i === selectedSizeIndex,
          }"
          v-on:click="selectSize(i)"
        >
          {{ sizeData.size }}
        </li>
      </ul>
      <!-- QUANTITY -->
      <div class="qty-container">
        <label>Quantity:</label>
        <select class="qty" id="quantity" v-model="selectedQty">
          <option
            v-for="num in product.sizes[selectedSizeIndex].stockCount"
            :key="num"
            :value="num"
            >{{ num }}</option
          >
        </select>
      </div>
      <div class="description">{{ product.description }}</div>
      <!-- PRICE AND BTN -->
      <div class="price">
        <div>{{ product.sizes[selectedSizeIndex].price }} $</div>
        <button
          v-on:click="
            addToCart({
              id: product.id,
              title: product.title,
              qty: selectedQty,
              size: product.sizes[selectedSizeIndex].size,
              image: product.images[0],
              price: product.sizes[selectedSizeIndex].price,
            })
          "
          :class="product.color"
        >
          Add to Bag
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    product: Object,
  },
  data() {
    return {
      selectedSizeIndex: 0,
      selectedQty: 1,
      selectedImgIndex: 0,
    }
  },
  methods: {
    addToCart(product) {
      this.$emit('addToCart', { ...product })
    },
    selectSize(i) {
      if (this.product.sizes[i].inStock) {
        this.selectedSizeIndex = i
      }
    },
    changeImage(i) {
      this.selectedImgIndex = i
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.product-card {
  border: 1px solid #bebebe;
  padding: 10px;
  margin: 20px auto;
  display: flex;
  max-width: 450px;
  border-radius: 3px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.left {
  background-color: #fff;
  border-radius: 3px;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
  padding: 10px;
  display: flex;
  flex-direction: column;
  grid-template-rows: auto auto;
  justify-content: space-evenly;
}
.img-container {
  width: 240px;
  padding: 1px;
}

.img {
  width: 100%;
  height: 180px;
  object-fit: cover;
  border-radius: 3px;
}
.img-preview-container {
  display: flex;
  margin-top: 10px;
  justify-content: center;
}

.preview {
  border: 1px solid #bebebe;
  margin: 2px;
  cursor: pointer;
}

.thumbnail {
  width: 50px;
}

.right {
  background-color: #fff;
  border-radius: 3px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}

h3 {
  padding: 5px;
  font-size: 18px;
  font-weight: 600;
  text-align: center;
  letter-spacing: -0.25px;
}
ul {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 0;
  padding: 10px;
}
li {
  width: 30px;
  padding: 3px;
  margin: 1px;
  border: 1px solid #ebebeb;
  border-radius: 3px;
  cursor: pointer;
  text-align: center;
}

.selected {
  box-shadow: rgb(17 17 17) 0px 0px 0px 1px inset;
}

li:hover {
  box-shadow: rgb(17 17 17) 0px 0px 0px 1px inset;
}

.sold-out {
  text-decoration: line-through;
  color: rgb(221, 221, 221);
  background: rgb(247, 247, 247);
  cursor: default;
}

.sold-out:hover {
  box-shadow: none;
}

.qty-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin: 5px auto;
}

label {
  margin-right: 5px;
}

.qty {
  width: 100%;
  text-align: center;
  margin: 0 auto;
}

.description {
  padding: 10px 0;
  font-size: 14px;
}

.price {
  display: flex;
  align-items: center;
}

.price div {
  display: flex;
  flex: 1;
  justify-content: center;
  align-items: center;
}

button {
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
}

button:hover {
  opacity: 0.8;
}

.pink {
  background-color: #e1cccb;
  color: #000;
}

.btn-pink {
  color: #e1cccb;
}

.blue {
  background-color: #add8e6;
}

.btn-blue {
  color: #4685b4;
}

.green {
  background-color: #c1e1c1;
}

.btn-green {
  color: #595f52;
}

.purple {
  background-color: #cbc3e3;
}

.btn-purple {
  color: #8667a9;
}
select {
  border: 1px solid #ddd;
  border-radius: 3px;
  cursor: pointer;
}
</style>
