<template>
      <div class="card p-3">
          <h3 class="mb-3">Add Transaction</h3>
              <form @submit.prevent="addTransaction">
                    <div class="mb-2">
                            <label class="form-label">Title</label>
                                    <input v-model="title" type="text" class="form-control" required />
                                          </div>
                                                <div class="mb-2">
                                                        <label class="form-label">Amount ($)</label>
                                                                <input v-model.number="amount" type="number" class="form-control" required min="1" />
                                                                      </div>
                                                                            <div class="mb-2">
                                                                                    <label class="form-label">Type</label>
                                                                                            <select v-model="type" class="form-control">
                                                                                                      <option value="INCOME">Income</option>
                                                                                                                <option value="EXPENSE">Expense</option>
                                                                                                                        </select>
                                                                                                                              </div>
                                                                                                                                    <button type="submit" class="btn btn-primary w-100">Add</button>
                                                                                                                                        </form>
                                                                                                                                          </div>
                                                                                                                                          </template>

                                                                                                                                          <script>
                                                                                                                                          import { ref } from 'vue';

                                                                                                                                          export default {
                                                                                                                                            emits: ['transaction-added'],
                                                                                                                                              setup(props, { emit }) {
                                                                                                                                                  const title = ref('');
                                                                                                                                                      const amount = ref(null);
                                                                                                                                                          const type = ref('INCOME');

                                                                                                                                                              const addTransaction = () => {
                                                                                                                                                                    if (!title.value || amount.value <= 0) {
                                                                                                                                                                            alert('Please enter a valid transaction');
                                                                                                                                                                                    return;
                                                                                                                                                                                          }

                                                                                                                                                                                                const newTransaction = {
                                                                                                                                                                                                        id: Date.now(),
                                                                                                                                                                                                                title: title.value,
                                                                                                                                                                                                                        amount: amount.value,
                                                                                                                                                                                                                                type: type.value.toUpperCase(),
                                                                                                                                                                                                                                      };

                                                                                                                                                                                                                                            emit('transaction-added', newTransaction);
                                                                                                                                                                                                                                                  
                                                                                                                                                                                                                                                        // Reset form fields
                                                                                                                                                                                                                                                              title.value = '';
                                                                                                                                                                                                                                                                    amount.value = null;
                                                                                                                                                                                                                                                                          type.value = 'INCOME';
                                                                                                                                                                                                                                                                              };

                                                                                                                                                                                                                                                                                  return { title, amount, type, addTransaction };
                                                                                                                                                                                                                                                                                    }
                                                                                                                                                                                                                                                                                    };
                                                                                                                                                                                                                                                                                    </script>