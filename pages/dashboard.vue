<template>
  <div class="min-h-screen bg-gray-50">
    <Navbar />
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
        <div class="card p-6">
          <h3 class="text-lg font-medium text-gray-900 mb-2">Total Customers</h3>
          <p class="text-3xl font-bold text-indigo-600">{{ totalCustomers }}</p>
        </div>
        <div class="card p-6">
          <h3 class="text-lg font-medium text-gray-900 mb-2">Total Amount</h3>
          <p class="text-3xl font-bold text-indigo-600">${{ totalAmount }}</p>
        </div>
        <div class="card p-6">
          <h3 class="text-lg font-medium text-gray-900 mb-2">Pending Payments</h3>
          <p class="text-3xl font-bold text-red-600">{{ pendingPayments }}</p>
        </div>
      </div>
      
      <CustomerTable />
    </div>
  </div>
</template>

<script>
export default {
  middleware: 'auth',
  computed: {
    totalCustomers() {
      return this.$children[1].$data.customers.length
    },
    totalAmount() {
      return this.$children[1].$data.customers
        .reduce((sum, customer) => sum + customer.amount, 0)
        .toFixed(2)
    },
    pendingPayments() {
      return this.$children[1].$data.customers
        .filter(customer => customer.status === 'due')
        .length
    }
  }
}
</script>