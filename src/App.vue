<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpenses :income="+income" :expenses="+expenses" />
      <TransactionList :transactions="transactions" />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed } from "vue";

const transactions = ref([
  { id: 1, text: "Flower", amount: -19.99 },
  { id: 2, text: "Salary", amount: 299.95 },
  { id: 3, text: "Book", amount: -15 },
  { id: 4, text: "Pen", amount: 90 },
]);

// Get Total
// console.log(transactions.value);
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});
// Get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});
// Get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

// Add transaction

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generatedUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  console.log(generatedUniqueId());
};

//  generatedUniqueId
const generatedUniqueId = () => {
  return Math.floor(Math.random() * 100000);
};
</script>
