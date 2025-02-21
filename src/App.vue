<template>
      <div class="container my-4">
          <h2 class="text-center">Expense Tracker</h2>

              <AddTransaction @transaction-added="addTransaction" />

                  <TransactionList :transactions="transactions" @transaction-deleted="deleteTransaction" />
                    </div>
                    </template>

                    <script>
                    import { ref, onMounted, watch } from 'vue';
                    import AddTransaction from './components/AddTransaction.vue';
                    import TransactionList from './components/TransactionList.vue';

                    export default {
                      components: { AddTransaction, TransactionList },
                        setup() {
                            const transactions = ref([]);

                                const loadTransactions = () => {
                                      const savedTransactions = localStorage.getItem('transactions');
                                            transactions.value = savedTransactions ? JSON.parse(savedTransactions) : [];
                                                };

                                                    const saveTransactions = () => {
                                                          localStorage.setItem('transactions', JSON.stringify(transactions.value));
                                                              };

                                                                  const addTransaction = (transaction) => {
                                                                        transactions.value.push(transaction);
                                                                              saveTransactions();
                                                                                  };

                                                                                      const deleteTransaction = (id) => {
                                                                                            transactions.value = transactions.value.filter((t) => t.id !== id);
                                                                                                  saveTransactions();
                                                                                                      };

                                                                                                          onMounted(loadTransactions);
                                                                                                              watch(transactions, saveTransactions, { deep: true });

                                                                                                                  return { transactions, addTransaction, deleteTransaction };
                                                                                                                    }
                                                                                                                    };
                                                                                                                    </script>