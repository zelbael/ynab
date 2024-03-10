<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }} <span>${{ transaction.amount }}</span>
      <button class="edit-btn" @click="openEditModal(transaction)">
        Edit
      </button>
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">
        x
      </button>
    </li>
  </ul>
  <EditTransactionModal :transaction="selectedTransaction" v-if="isEditModalOpen" @close="closeEditModal" @update="handleTransactionEdited" />
</template>

<script setup>
import { defineProps, defineEmits } from "vue";
import EditTransactionModal from "./EditTransactionModal.vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["transactionDeleted", "transactionEdited"]);

let isEditModalOpen = false;
let selectedTransaction = null;

const openEditModal = (transaction) => {
  selectedTransaction = transaction;
  isEditModalOpen = true;
};

const closeEditModal = () => {
  isEditModalOpen = false;
};

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};

const handleTransactionEdited = (updatedTransaction) => {
  // Emit the updated transaction to the parent component
  emit("transactionEdited", updatedTransaction);
};
</script>
