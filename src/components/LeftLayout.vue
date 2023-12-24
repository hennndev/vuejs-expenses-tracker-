<script>
    import Header from './Header.vue';
    import Balances from './Balances.vue';
    import AddTransactionVue from './AddTransaction.vue'
    export default {
        props: ['balance', 'transactions', 'handleAddTransaction'],
        components: {
            Header,
            Balances,
            AddTransactionVue
        }
    }
    </script>
<template>
    <section class="sticky top-5 h-full w-[400px] shadow-sm rounded-md p-5">
        <Header/>
        <Balances 
            :balance="this.balance"
            :transactions="this.transactions"/>
        <AddTransactionVue
            :transactions="this.transactions"
            :handleAddTransaction="this.handleAddTransaction"/>
    </section>
</template>
