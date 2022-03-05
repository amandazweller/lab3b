<template>
<div class="wrapper">
  <div class="products">
    <div class="product" v-for="product in this.$root.$data.cart" :key="product.id">
      <div class="info">
        <h1>{{product.name}}</h1>
        <h2>Quantity: {{product.quantity}}</h2>
      </div>
      <div class="image">
        <img :src="'/images/products/'+product.image">
      </div>
      <div class="price">
        <h2>{{product.price}}</h2>
        <button v-on:click="removeFromCart(product)">Remove From Cart</button>
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'CartList',
  props: {
    cart: Array
  },
  methods:  {
    removeFromCart: function(product) {
      this.$root.$data.numItems = 0;
      for (let index in this.$root.$data.cart){
        this.$root.$data.numItems += 
        this.$root.$data.cart[index].quantity;
      }
      for (let index in this.$root.$data.cart){
        if(this.$root.$data.cart[index].id == product.id){
          if(this.$root.$data.cart[index].quantity > 1){
            this.$root.$data.cart[index].quantity -= 1;
            this.$root.$data.numItems -= 1;
          }
          else{
            this.$root.$data.cart.splice(index, 1);
            this.$root.$data.numItems -= 1;
          }
          break
          } 
        }
      },
    },
  };
</script>
<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.products {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.product {
  margin: 10px;
  margin-top: 50px;
  width: 200px;
}

.product img {
  border: 1px solid #333;
  height: 250px;
  width: 200px;
  object-fit: cover;
}

.product .image {
  display: flex;
  justify-content: center;
  margin-bottom: 5px;
}

.info {
  background: #000;
  color: white;
  padding: 10px 30px;
  height: 80px;
}

.info h1 {
  font-size: 16px;
}

.info h2 {
  font-size: 14px;
}

.info p {
  margin: 0px;
  font-size: 10px;
}
.price {
  display: flex;
  padding: 2%;
}

button {
  height: 50px;
  background: #000;
  color: white;
  border: none;
}

.auto {
  margin-left: auto;
}
</style>
