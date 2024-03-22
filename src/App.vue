<template>
  <div id="app">
    <div class="container">
      <div class="products">
        <h2>Product List</h2>
        <table>
          <tr>
            <th class = "tag1" id="pTag">Product</th>
            <th class = "tag">Price</th>
          </tr>
          <tr v-for="product in products" :key="product.id">
            <td class="pName">{{ product.name }}</td>
            <td>₱ {{ product.price }}</td>
            <td><button @click="addToCart(product)" class="btnAdd">Add to Cart</button></td>
          </tr>
        </table>
      </div>
      <div class="cart">
        <div v-if="cart.length === 0">

        </div>
        <div v-else>
          <cart-item v-for="(item, index) in cart" :key="index" :item="item" @remove-from-cart="removeCart(index)" @update-quantity="updateQuantity(index)"></cart-item>
          <p>Total Amount: ₱{{ total }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import CartItem from './components/CartItem.vue';

export default {
  components: {
    CartItem
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Constantine', price: 21000 },
        { id: 2, name: 'tsunami', price: 16000 },
        { id: 3, name: 'The Project', price: 15000 },
        { id: 4, name: 'Scalawag', price: 15000 },
        { id: 5, name: 'Skream', price:  20000 },
        { id: 6, name: 'Carbon Nation Cycling', price: 20000 },
        { id: 7, name: 'Navigate Tri-spokes', price: 5000 },
        { id: 8, name: 'Navigate Five-spokes', price: 5000 },
        { id: 9, name: 'Envy', price: 15000 },
        { id: 10, name: 'Zipp', price: 30000 }

      ],
      cart: []
    };
  },
  computed: {
    total() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
    }
  },
  methods: {
    addToCart(product) {
      let existingItem = this.cart.find(item => item.id === product.id);
      if (existingItem) {
        existingItem.quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      if (this.cart[index].quantity < 1) {
        this.cart[index].quantity = 1;
      }
    }
  }
};
</script>

<style scoped>
.container {
  position: absolute;
  top: 0%;
  left: 10%;

  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: left;
  margin-top: 100px;
}

.products, .cart {
  color: rgb(0, 0, 0);
  text-align: center;
  width: 100%,100%;
  max-width: 800px;
  border: 1px solid #000000;
  padding: 50px;
 
}

.products table, .cart table {
  border-color: rgb(255, 252, 252);
  width: 100%;
  border-collapse: collapse;
}

.products th, .products td, .cart th, .cart td {
  border: 1px solid #13121200;
  /* padding: 10px;              para ito sa padding*/
  margin-right: 10px;
}

.products button {
  cursor: pointer;
}
h2{
  font-weight: bold;
  font-size: 40px;
  color: #ff3c00;
}

.tag{
  font-weight: bold;
}

.pName{
  text-align: left;
  margin: 10px;
  padding-right: 130px;

}


.pName:hover{
    font-size: 25px; 
    cursor: pointer;
    color: #ff3c00;
    transition: font-size 0.3s ease;
}

.tag1{
  font-weight: bold;
  text-align: left;
  margin: 10px;
}



td{
  font-size: 18px;
}





.btnAdd{
  background-color: #ff6f00;
  color: white;
  border-radius: 5px;
  border-color: rgb(255, 255, 255);
  width: 100px;
  height: 30px;
}

.btnAdd:hover{
  background-color: #bb5202;
  color: white;
  border-radius: 5px;
  border-color: rgb(255, 255, 255);
}


</style>
