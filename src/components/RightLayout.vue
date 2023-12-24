<script>
    import TransactionsTable from './TransactionsTable.vue';
    import HeaderTable from './HeaderTable.vue';
    export default {
        props: ['transactions'],
        components: {
            TransactionsTable,
            HeaderTable
        }
    }
</script>

<template>
    <section class="sticky top-5 h-full flex-1 shadow-sm rounded-md p-5">
        <HeaderTable/>
        <TransactionsTable :transactions="this.transactions"/>
    </section>
</template>


