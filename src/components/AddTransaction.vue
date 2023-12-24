<script>
    export default {
        data() {
            return {
                transactionValues: {
                    transactionName: '',
                    transactionCategory: 'income',
                    costCategory: '',
                    transactionCost: '',
                    transactionDescription: ''
                },
                errors: {}
            }
        },
        props: ['handleAddTransaction'],
        methods: {
            handleBlur(fieldName) {
                if(this.transactionValues[fieldName]) {
                    this.errors[fieldName] = ''
                } else {
                    const errors = this.handleErrors()
                    this.errors = errors
                }
            },
            handleErrors() {
                let errors = {}
                const {
                    transactionName, transactionCategory, costCategory, transactionCost, transactionDescription
                 } = this.transactionValues
                if(transactionName === '') {
                    errors.transactionName = true
                } else {
                    delete errors.transactionName
                }

                if(transactionCategory === '') {
                    errors.transactionCategory = true
                } else {
                    delete errors.transactionCategory
                }

                if(costCategory === '') {
                    errors.costCategory = true
                } else {
                    delete errors.costCategory
                }

                if(!transactionCost) {
                    errors.transactionCost = true
                } else {
                    delete errors.transactionCost
                }

                if(transactionDescription === '') {
                    errors.transactionDescription = true
                } else {
                    delete errors.transactionDescription
                }
                return errors
            },
            handleSubmit() {
                const errors = this.handleErrors()
                this.errors = errors
                if(Object.keys(errors).length < 1) {
                    this.handleAddTransaction({
                        id: new Date().getTime(),
                        date: new Date(),
                        ...this.transactionValues
                    }) 
                } 
            }
        },
        
    }
</script>

<template>
    <section class="mt-5">
        <form @submit.prevent="handleSubmit" class="flex flex-col">
            <p class="mb-3">Add Transaction</p>
            <div class="mb-3">
                <select 
                    name="transactionCategory" 
                    v-model="transactionValues.transactionCategory" 
                    :class="[errors.transactionCategory ? 'border-red-500' : '' , 'w-full input-control']">
                    <option value="income">Income</option>
                    <option value="expenses">Expenses</option>
                </select>
            </div>
            <div class="mb-3">
                <input 
                    type="text"
                    name="transactionName" 
                    v-model="transactionValues.transactionName"
                    placeholder="Transaction title" 
                    @blur="handleBlur('transactionName')"
                    :class="[errors.transactionName && 'border-2 border-red-300 focus:ring-0 focus:border-2 focus:border-red-300' , 'w-full input-control']">
            </div>
            <div class="mb-3">
                <select 
                    name="costCategory" 
                    v-model="transactionValues.costCategory"
                    @blur="handleBlur('costCategory')"
                    :class="[errors.costCategory && 'border-2 border-red-300 focus:ring-0 focus:border-2 focus:border-red-300' , 'w-full input-control']">
                    <option value="" selected>Cost Category</option>
                    <option value="food">Food</option>
                    <option value="life style">Life Style</option>
                    <option value="financial">Financial</option>
                </select>
            </div>
            <div class="mb-3">
                <textarea 
                    name="transactionDescription" 
                    v-model="transactionValues.transactionDescription"
                    rows="5" 
                    @blur="handleBlur('transactionDescription')"
                    :class="[errors.transactionDescription && 'border-2 border-red-300 focus:ring-0 focus:border-2 focus:border-red-300' , 'w-full input-control']"
                    placeholder="Description transaction"></textarea>
            </div>
            <div class="mb-3">
                <input 
                    type="number" 
                    name="transactionCost"
                    v-model="transactionValues.transactionCost"    
                    placeholder="Cost" 
                    @blur="handleBlur('transactionCost')"
                    :class="[errors.transactionCost && 'border-2 border-red-300 focus:ring-0 focus:border-2 focus:border-red-300' , 'w-full input-control']">
            </div>
            <button type="submit" class="border-none outline-none bg-blue-300 text-gray-700 rounded-md p-3 font-semibold hover:bg-blue-500 hover:text-white">
                Submit
            </button>
        </form>
    </section>
</template>

