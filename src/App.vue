<script>
    import LeftLayout from './components/LeftLayout.vue';
    import RightLayout from './components/RightLayout.vue';
    export default {
        data() {
            return {
                balance: JSON.parse(localStorage.getItem('balance')) || 0,
                transactions: JSON.parse(localStorage.getItem('transactions')) || [],
                transaction: {},
            }
        },
        watch: {
            transactions() {
                this.balance = this.transactions?.filter(tr => tr.transactionCategory === 'income').reduce((currVal, val) => {
                    return currVal += val.transactionCost
                }, 0) - this.transactions?.filter(tr => tr.transactionCategory === 'expenses').reduce((currVal, val) => {
                    return currVal += val.transactionCost
                }, 0)
                localStorage.setItem('balance', JSON.stringify(this.balance))
            }
        },
        methods: {
            handleAddTransaction(transaction) {
                const checkExist = this.transactions.find(tr => tr.id === transaction.id)
                if(checkExist) {
                    this.transactions = this.transactions.map(tr => {
                        if(tr.id === transaction.id) {
                            return {
                                ...tr,
                                ...transaction
                            }
                        } else {
                            return tr
                        }
                    })
                } else {
                    this.transactions = [...this.transactions, transaction]
                }
                localStorage.setItem('transactions', JSON.stringify(this.transactions))
            },
            handleEditTransaction(id) {
                const transaction = this.transactions.find(tr => tr.id === id)
                this.transaction = transaction
            },
            handleDeleteTransaction(id) {
                this.transactions = this.transactions.filter(tr => tr.id !== id)
                localStorage.setItem('transactions', JSON.stringify(this.transactions))
            }
        },
        components: {
            LeftLayout,
            RightLayout
        }
    }
</script>


<template>
    <main class="container flex flex-col lg:flex-row px-5 mt-5 mb-5 lg:space-x-5">
        <LeftLayout 
            :transaction="this.transaction"
            :balance="this.balance"
            :transactions="this.transactions"
            :handleAddTransaction="this.handleAddTransaction"/>
        <RightLayout
            :handleEditTransaction="this.handleEditTransaction"
            :handleDeleteTransaction="this.handleDeleteTransaction"
            :transactions="this.transactions"/>
    </main>
</template>

