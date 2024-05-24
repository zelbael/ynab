# ynab
# You Need A Budget: Expense Tracker

<img width="528" alt="Screenshot 2024-03-10 at 3 59 33 PM" src="https://github.com/zelbael/ynab/assets/127542906/4864fda9-05d0-4faa-bb6b-882cea924f32">


Expense Tracker is a simple web application that helps users track their income and expenses. It allows users to add, edit, and delete transactions, and provides a balance overview.

## Features

- **Transaction Management:** Users can add, edit, and delete transactions.
- **Balance Overview:** Users can view their total balance, income, and expenses.
- **LocalStorage:** Transactions are saved in the browser's localStorage for persistence across sessions.

## Technologies Used

- **Vue.js:** The frontend of the application is built using Vue.js, a progressive JavaScript framework.
- **Vue Toastification:** For displaying toast messages for user actions.

## Project Structure

The project is organized into the following components:

- **Header.vue:** Component for the header of the application.
- **Balance.vue:** Component for displaying the total balance.
- **IncomeExpenses.vue:** Component for displaying income and expenses.
- **TransactionList.vue:** Component for displaying the list of transactions.
- **AddTransaction.vue:** Component for adding new transactions.
- **EditTransactionModal.vue:** Component for editing transactions.
