<template>
  <div>
    <Header />
    <div class="container">
      <Balance :total="total" />
      <IncomeExpenses :income="+income" :expenses="+expenses" />
      <TransactionList
        :transactions="transactions"
        @transactionDeleted="handleTransactionDeleted"
        @transactionEdited="handleTransactionEdited"
      />
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
    <EditTransactionModal :transaction="selectedTransaction" v-if="isEditModalOpen" @close="closeEditModal" @update="handleTransactionEdited" />
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';
import EditTransactionModal from './components/EditTransactionModal.vue';

import { ref, computed, onMounted } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();
const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

// submit transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success('Transaction added.');
};

// handle editing transaction
const handleTransactionEdited = (editedTransaction) => {
  const index = transactions.value.findIndex((t) => t.id === editedTransaction.id);
  transactions.value[index] = { ...editedTransaction };

  saveTransactionsToLocalStorage();

  toast.success('Transaction edited.');
};

// delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  toast.success('Transaction deleted.');
};

// generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};

// edit transaction modal
const isEditModalOpen = ref(false);
const selectedTransaction = ref(null);

const openEditModal = (transaction) => {
  selectedTransaction.value = transaction;
  isEditModalOpen.value = true;
};

const closeEditModal = () => {
  isEditModalOpen.value = false;
};
</script>
