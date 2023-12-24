<script>
    export default {
        props: ['balance', 'transactions'],
        methods: {
            getTotalCost(costCty) {
                return this.transactions?.filter(tr => tr.transactionCategory === costCty).reduce((currVal, val) => {
                    return currVal += val.transactionCost
                }, 0)
            },
        }
    }
</script>

<template>
    <section class="mt-5">
        <p class="text-gray-700">Current Balance</p>
        <h1 class="font-bold text-gray-800 text-xl mt-2">Rp{{this.balance}}</h1>
        <div class="mt-5 flex flex-col space-y-3">
            <!-- Income -->
            <div class="bg-green-100 rounded-md p-3 flexx">
                <div class="p-3 rounded-xl bg-green-300 mr-4">
                    <i class="pi pi-wallet text-xl text-gray-700"></i>
                </div>
                <div class="">
                    <p class="text-gray-700">Income</p>
                    <h2 class="font-semibold text-gray-800">Rp{{ this.getTotalCost('income') }}</h2>
                </div>
            </div>
            <div class="bg-red-100 rounded-md p-3 flexx">
                <div class="p-3 rounded-xl bg-red-300 mr-4">
                    <i class="pi pi-dollar text-xl text-gray-700"></i>
                </div>
                <div class="">
                    <p class="text-gray-700">Expenses</p>
                    <h2 class="font-semibold text-gray-800">Rp{{ this.getTotalCost('expenses') }}</h2>
                </div>
            </div>
        </div>
    </section>
</template>

