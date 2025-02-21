<template>
      <div class="card p-3 mt-3">
          <h3 class="mb-3">Transaction List</h3>

              <div class="mb-3">
                    <label>Filter:</label>
                          <select v-model="filter" class="form-select">
                                  <option value="ALL">All</option>
                                          <option value="INCOME">Income</option>
                                                  <option value="EXPENSE">Expense</option>
                                                        </select>
                                                            </div>

                                                                <table class="table table-bordered">
                                                                      <thead class="table-dark">
                                                                              <tr>
                                                                                        <th>Title</th>
                                                                                                  <th>Amount ($)</th>
                                                                                                            <th>Type</th>
                                                                                                                      <th>Action</th>
                                                                                                                              </tr>
                                                                                                                                    </thead>
                                                                                                                                          <tbody>
                                                                                                                                                  <tr v-for="transaction in filteredTransactions" :key="transaction.id">
                                                                                                                                                            <td>{{ transaction.title }}</td>
                                                                                                                                                                      <td :class="amountClass(transaction)">${{ transaction.amount }}</td>
                                                                                                                                                                                <td :class="typeClass(transaction)">{{ transaction.type }}</td>
                                                                                                                                                                                          <td>
                                                                                                                                                                                                      <button class="btn btn-danger btn-sm" @click="deleteTransaction(transaction.id)">Delete</button>
                                                                                                                                                                                                                </td>
                                                                                                                                                                                                                        </tr>
                                                                                                                                                                                                                                <tr v-if="filteredTransactions.length === 0">
                                                                                                                                                                                                                                          <td colspan="4" class="text-center">No transactions recorded yet.</td>
                                                                                                                                                                                                                                                  </tr>
                                                                                                                                                                                                                                                        </tbody>
                                                                                                                                                                                                                                                            </table>
                                                                                                                                                                                                                                                              </div>
                                                                                                                                                                                                                                                              </template>

                                                                                                                                                                                                                                                              <script>
                                                                                                                                                                                                                                                              import { ref, computed, watch } from 'vue';

                                                                                                                                                                                                                                                              export default {
                                                                                                                                                                                                                                                                props: ['transactions'],
                                                                                                                                                                                                                                                                  emits: ['transaction-deleted'],
                                                                                                                                                                                                                                                                    setup(props, { emit }) {
                                                                                                                                                                                                                                                                        const filter = ref('ALL');

                                                                                                                                                                                                                                                                            const filteredTransactions = computed(() => {
                                                                                                                                                                                                                                                                                  if (filter.value === 'ALL') return props.transactions;
                                                                                                                                                                                                                                                                                        return props.transactions.filter((t) => t.type === filter.value);
                                                                                                                                                                                                                                                                                            });

                                                                                                                                                                                                                                                                                                const deleteTransaction = (id) => {
                                                                                                                                                                                                                                                                                                      emit('transaction-deleted', id);
                                                                                                                                                                                                                                                                                                          };

                                                                                                                                                                                                                                                                                                              const typeClass = (transaction) => ({
                                                                                                                                                                                                                                                                                                                    'text-success': transaction.type === 'INCOME',
                                                                                                                                                                                                                                                                                                                          'text-danger': transaction.type === 'EXPENSE',
                                                                                                                                                                                                                                                                                                                              });

                                                                                                                                                                                                                                                                                                                                  const amountClass = (transaction) => ({
                                                                                                                                                                                                                                                                                                                                        'fw-bold': transaction.amount >= 500,
                                                                                                                                                                                                                                                                                                                                            });

                                                                                                                                                                                                                                                                                                                                                return { filter, filteredTransactions, deleteTransaction, typeClass, amountClass };
                                                                                                                                                                                                                                                                                                                                                  }
                                                                                                                                                                                                                                                                                                                                                  };
                                                                                                                                                                                                                                                                                                                                                  </script>