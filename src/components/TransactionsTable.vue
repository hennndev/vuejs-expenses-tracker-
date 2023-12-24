<script>
    export default {
        props: ['transactions']
    }
</script>


<template>
    <div class="relative overflow-x-auto shadow-sm sm:rounded-lg">
        <table class="w-full text-sm text-left">
            <thead class="text-gray-700">
                <tr>
                    <th scope="col" class="px-6 py-3 font-normal text-gray-700">
                        Transaction name
                    </th>
                    <th scope="col" class="px-6 py-3 font-normal text-gray-700">
                        Category
                    </th>
                    <th scope="col" class="px-6 py-3 font-normal text-gray-700">
                        Cost
                    </th>
                    <th scope="col" class="px-6 py-3 font-normal text-gray-700">
                        Description
                    </th>
                    <th scope="col" class="px-6 py-3 font-normal text-gray-700">
                        Action
                    </th>
                </tr>
            </thead>
            <tbody>
                <template v-for="tr in transactions" :key="tr.id">
                    <tr :class="tr.transactionCategory === 'expenses' ? 'bg-red-50' : 'bg-green-50'">
                        <th scope="row" class="px-6 py-4 font-medium text-gray-700 whitespace-nowrap">
                            {{ tr.transactionName }}
                        </th>
                        <td class="px-6 py-4 text-gray-700 font-medium">
                            {{ tr.costCategory }}
                        </td>
                        <td class="px-6 py-4 text-gray-700 font-medium">
                            Rp{{ tr.transactionCost }}
                        </td>
                        <td class="px-6 py-4 text-gray-700">
                            Description
                        </td>
                        <td class="px-6 py-4">
                            <a href="#" class="font-medium text-blue-600 hover:underline mr-3">Edit</a>
                            <a href="#" class="font-medium text-red-600 hover:underline">Delete</a>
                        </td>
                    </tr>
                </template>
            </tbody>
        </table>
    </div>
</template>


