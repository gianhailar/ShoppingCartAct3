<template>
    <div class="cart-item">
      <table>
        <tr>
          <th>Item </th>
          <th>Price</th>
          <th>Quantity</th>
          <th>Cancel Order</th>
        </tr>
        <tr>
          <td>{{ item.name }}</td>
          <td>₱ {{ item.price }}</td>
          <td>
            <div class="quantity">
              <button @click="updateQuantity('decrement')">-</button>
             
              <span>{{ item.quantity }}</span>
              <button @click="updateQuantity('increment')">+</button>
            </div>
          </td>
          <td>
            <button @click="removeFromCart" class="btnCancel">Cancel</button>
          </td>
        </tr>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    methods: {
      removeFromCart() {
        this.$emit('remove-from-cart');
      },
      updateQuantity(action) {
        if (action === 'increment') {
          this.item.quantity++;
        } else if (action === 'decrement' && this.item.quantity > 1) {
          this.item.quantity--;
        }
        this.$emit('update-quantity');
      }
    }
  };
  </script>
  
  <style scoped>
  .cart-item {
    margin-bottom: 10px;
  }
  
  table {
    width: 100%;
    border-collapse: collapse;
  }
  
  th, td {
    width: 100%;
    border: 1px solid #ddd;
    padding: 8px;
    text-align: center;
  }
  
  th {
    background-color: #ff4800f8;
  }
  
  .quantity {
    display: flex;
    align-items: center;
  }
  
  .quantity button {
    padding: 4px 8px;
    margin: 0 4px;
    border: none;
    background-color: #fffffff8;
    color: rgb(255, 0, 0);
    cursor: pointer;
    font-size: 20px;
  }
  
  .quantity button:hover {
    background-color: #ff4800f8;
    color: rgb(255, 255, 255);
  }



  
.btnCancel{
  background-color: #ff0000;
  color: white;
  border-radius: 5px;
  border-color: rgb(255, 255, 255);
  width: 100px;
  height: 30px;
}

.btnCancel:hover{
  background-color: #bb0202;
  color: white;
  border-radius: 5px;
  border-color: rgb(255, 255, 255);
}

  </style>