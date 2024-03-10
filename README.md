# ynab
# You Need A Budget: Expense Tracker

Expense Tracker is a simple web application that helps users track their income and expenses. It allows users to add, edit, and delete transactions, and provides a balance overview.

## Features

- **Transaction Management:** Users can add, edit, and delete transactions.
- **Balance Overview:** Users can view their total balance, income, and expenses.
- **LocalStorage:** Transactions are saved in the browser's localStorage for persistence across sessions.

## Technologies Used

- **Vue.js:** The frontend of the application is built using Vue.js, a progressive JavaScript framework.
- **Vue Toastification:** For displaying toast messages for user actions.
- **SCSS:** Styling is done using SCSS preprocessor.
- **LocalStorage API:** Used to store transactions locally in the browser.

## Project Structure

The project is organized into the following components:

- **Header.vue:** Component for the header of the application.
- **Balance.vue:** Component for displaying the total balance.
- **IncomeExpenses.vue:** Component for displaying income and expenses.
- **TransactionList.vue:** Component for displaying the list of transactions.
- **AddTransaction.vue:** Component for adding new transactions.
- **EditTransactionModal.vue:** Component for editing transactions.

## Usage

To run the Expense Tracker locally:

1. Clone this repository.
2. Navigate to the project directory.
3. Install dependencies using `npm install`.
4. Run the development server using `npm run serve`.
5. Access the application in your browser at `http://localhost:8080`.
