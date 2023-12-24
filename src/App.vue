<script>
    import LeftLayout from './components/LeftLayout.vue';
    import RightLayout from './components/RightLayout.vue';
    export default {
        data() {
            return {
                balance: JSON.parse(localStorage.getItem('balance')) || 0,
                transactions: JSON.parse(localStorage.getItem('transactions')) || []
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
                this.transactions = [...this.transactions, transaction]
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
    <main class="container flex px-5 mt-5 mb-5 space-x-5">
        <LeftLayout 
            :balance="this.balance"
            :transactions="this.transactions"
            :handleAddTransaction="this.handleAddTransaction"/>
        <RightLayout
            :transactions="this.transactions"/>
    </main>
</template>

