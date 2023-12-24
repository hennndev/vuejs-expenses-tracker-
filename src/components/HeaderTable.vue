<script>
    export default {
        data() {
            return {
                searchTerm: '',
                isFocus: false
            }
        },
        props: ['handleSortByTrCategory', 'handleSearch'],
        watch: {
            searchTerm() {
                console.log(this.searchTerm)
                this.handleSearch(this.searchTerm)
            }
        },
        methods: {
            handleBlur: function() {
                console.log(this.isFocus)
                this.isFocus = false
            },
            handleFocus: function() {
                this.isFocus = true
            },
            handleChangeCategory(event) {
                this.handleSortByTrCategory(event.target.value)
            },
        }
    }
</script>



<template>
    <div class="mb-5">
        <h1 class="mb-3 font-semibold text-gray-700">Transactions List</h1>
        <div class="flexx space-x-3">
            <div :class="[isFocus ? 'border-2 border-blue-300' : 'border border-gray-100', 'flex-1 flexx px-3 rounded-md']">
                <i class="pi pi-search text-sm text-gray-700"></i>
                <input 
                    v-model="searchTerm"
                    @focus="handleFocus()"
                    @blur="handleBlur()"
                    type="text" 
                    class="w-full py-2 border-none outline-none flex-1 focus:ring-0 text-gray-700 text-[15px]" 
                    placeholder="Search transaction">
            </div>
            <select @change="handleChangeCategory($event)" class="input-control mb-0 outline-none text-[15px] text-gray-700 flex-1">
                <option value="" @change="">Income/Outcome</option>
                <option value="income">Income</option>
                <option value="expenses">Expenses</option>
            </select>
        </div>
    </div>
</template>
