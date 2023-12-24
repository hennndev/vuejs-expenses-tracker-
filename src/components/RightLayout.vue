<script>
    import TransactionsTable from './TransactionsTable.vue';
    import HeaderTable from './HeaderTable.vue';
    export default {
        data() {
            return {
                searchTerm: '',
                trCategory: ''
            }
        },
        props: ['transactions', 'handleEditTransaction', 'handleDeleteTransaction'],
        components: {
            TransactionsTable,
            HeaderTable
        },
        computed: {
            updatedTransactions() {
                return this.transactions.filter(tr => tr.transactionCategory.includes(this.trCategory)).filter(tr => {
                    return tr.transactionName.toLowerCase().includes(this.searchTerm.toLowerCase()) ||
                    tr.transactionCategory.toLowerCase().includes(this.searchTerm.toLowerCase()) || 
                    tr.costCategory.toLowerCase().includes(this.searchTerm.toLowerCase()) ||
                    tr.transactionDescription.toLowerCase().includes(this.searchTerm.toLowerCase())
                })
            }
        },
        methods: {
            handleSearch(searchTerm) {
                this.searchTerm = searchTerm
            },
            handleSortByTrCategory(trCategory) {
                this.trCategory = trCategory
            }
        }
    }
</script>

<template>
    <section class="static mt-10 lg:mt-0 lg:sticky top-5 h-full flex-1 shadow-sm rounded-md p-5">
        <HeaderTable 
            :handleSearch="this.handleSearch"
            :handleSortByTrCategory="this.handleSortByTrCategory"/>
        <TransactionsTable 
            :transactions="this.updatedTransactions"
            :handleEditTransaction="this.handleEditTransaction"
            :handleDeleteTransaction="this.handleDeleteTransaction"/>
    </section>
</template>


