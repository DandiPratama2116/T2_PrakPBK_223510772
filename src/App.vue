<template>
  <div id="app">
    <h1>List Harga Barang</h1>
    
    <!-- Form untuk memasukkan pengeluaran baru -->
    <form @submit.prevent="addExpense" class="form">
      <label for="description">Nama barang:</label>
      <input type="text" id="description" v-model="newExpense.description" required>

      <label for="amount">Harga:</label>
      <input type="number" id="amount" v-model.number="newExpense.amount" required>

      <label for="quantity">
        Jumlah:
      </label>
      <div class="quantity-input">
        <input type="number" id="quantity" v-model.number="newExpense.quantity" required class="quantity-input-field">
        
      </div>

      <button type="submit" class="submit-button">Tambahkan</button>
    </form>

    <!-- Daftar pengeluaran -->
    <div class="expenses">
      <h2>List</h2>
      <ul>
        <li v-for="(expense, index) in expenses" :key="index" :class="{ 'highlight': expense.amount > limit }">
          <span class="description">{{ expense.description }}</span> 
          <span class="quantity">{{ expense.quantity }}</span>
          <span class="amount">{{ formatRupiah(expense.amount) }}</span>
          <button @click="deleteExpense(index)" class="delete-button">Hapus</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newExpense: {
        description: '',
        amount: '',
        quantity: 1
      },
      expenses: [],
      limit: 50000000
    };
  },
  methods: {
    addExpense() {
      this.expenses.push({...this.newExpense});
      this.newExpense.description = '';
      this.newExpense.amount = '';
      this.newExpense.quantity = 1;
    },
    deleteExpense(index) {
      this.expenses.splice(index, 1);
    },
    formatRupiah(amount) {
      return new Intl.NumberFormat('id-ID', { style: 'currency', currency: 'IDR' }).format(amount);
    },
    increaseQuantity() {
      this.newExpense.quantity++;
    },
    decreaseQuantity() {
      if (this.newExpense.quantity > 1) {
        this.newExpense.quantity--;
      }
    }
  }
};
</script>

<style scoped>
/* General styles */
body {
  font-family: 'Montserrat', sans-serif;
  margin: 0;
  padding: 0;
  background-color: #c1e90e;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #bf8c26;
}

h1 {
  text-align: center;
  color: #333;
  margin-bottom: 30px;
}

.form {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-bottom: 20px;
}

.form label {
  width: 100px;
}

.form input {
  flex: 1;
  padding: 8px;
  margin-bottom: 10px;
}

.submit-button {
  background-color: #e1eb29;
  color: #010300;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.submit-button:hover {
  background-color: #e51310;
}

.quantity-input {
  display: flex;
  align-items: center;
}

.quantity-input-field {
  padding: 8px;
  margin-right: 5px;
}

.quantity-button {
  background-color: #518434;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
  margin-left: 5px;
  font-family: 'Montserrat', sans-serif;
}

.quantity-button:hover {
  background-color: #336d16;
}

.expenses {
  background-color: #518434;
  border-radius: 10px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

.expenses h2 {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

.expenses ul {
  list-style: none;
  padding: 0;
}

.expenses li {
  border-bottom: 1px solid #9c464600;
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.expenses li:last-child {
  border-bottom: none;
}

.expenses .highlight {
  color: rgb(255, 0, 0);
}

.expenses .description {
  flex: 1;
}

.expenses .quantity {
  margin-right: 10px;
}

.expenses .amount {
  font-weight: bold;
}

.delete-button {
  background-color: #ff0000;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #cc0000;
}
</style>
