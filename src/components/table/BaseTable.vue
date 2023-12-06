<template>
    <!-- Table Section -->
    <div class="max-w-[85rem] px-4 py-10 sm:px-6 lg:px-8 lg:py-14 mx-auto">
        <!-- Card -->
        <div class="flex flex-col">
            <div class="-m-1.5 overflow-x-auto">
                <div class="p-1.5 min-w-full inline-block align-middle">
                    <div
                        class="bg-white border border-gray-200 rounded-xl shadow-sm overflow-hidden dark:bg-slate-900 dark:border-gray-700">
                        <!-- Header -->
                        <div
                            class="px-6 py-4 grid gap-3 md:flex md:justify-between md:items-center border-b border-gray-200 dark:border-gray-700">
                            <div>
                                <h2 class="text-xl font-semibold text-gray-800 dark:text-gray-200">
                                    Visitors
                                </h2>
                                <p class="text-sm text-gray-600 dark:text-gray-400">
                                    Visitors overview by country.
                                </p>
                            </div>

                        </div>
                        <!-- End Header -->

                        <!-- Table -->
                        <table class="min-w-full divide-y divide-gray-200 dark:divide-gray-700">
                            <thead class="bg-gray-50 divide-y divide-gray-200 dark:bg-gray-800 dark:divide-gray-700">
                                <tr>
                                    <th scope="col"
                                        class="px-6 py-3 text-start border-s border-gray-200 dark:border-gray-700">
                                        <span
                                            class="text-xs font-semibold uppercase tracking-wide text-gray-800 dark:text-gray-200">
                                            Country
                                        </span>
                                    </th>

                                    <th scope="col" class="px-6 py-3 text-start">
                                        <span
                                            class="text-xs font-semibold uppercase tracking-wide text-gray-800 dark:text-gray-200">
                                            Name
                                        </span>
                                    </th>

                                    <th scope="col" class="px-6 py-3 text-start">
                                        <span
                                            class="text-xs font-semibold uppercase tracking-wide text-gray-800 dark:text-gray-200">
                                            isActive
                                        </span>
                                    </th>
                                </tr>
                            </thead>

                            <tbody class="divide-y divide-gray-200 dark:divide-gray-700">
                                <tr v-for="(item, index) in tableData" :key="index">
                                    <td class="h-px w-auto whitespace-nowrap">
                                        <div class="px-6 py-2">
                                            <span class="font-semibold text-sm text-gray-800 dark:text-gray-200">{{
                                                item.country }}</span>
                                        </div>
                                    </td>
                                    <td class="h-px w-auto whitespace-nowrap">
                                        <div class="px-6 py-2">
                                            <span class="font-semibold text-sm text-gray-800 dark:text-gray-200">{{
                                                item.name }}</span>
                                        </div>
                                    </td>
                                    <td class="h-px w-auto whitespace-nowrap">
                                        <div class="px-6 py-2">
                                            <span class="text-sm text-gray-800 dark:text-gray-200">{{ item.isActive
                                            }}</span>
                                        </div>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                        <!-- End Table -->
                    </div>
                </div>
            </div>
        </div>
        <!-- End Card -->
    </div>
    <!-- End Table Section -->
</template>

<script>
export default {
    data() {
        return {
            tableData: [], // Array to store table data
            intervalId: null,
            counter: 0,
        };
    },
    mounted() {
        // Simulate a memory leak by creating a setInterval without clearing it
        this.intervalId = setInterval(() => {
            // Push new data to the tableData array
            if (this.counter <= 15) {
                this.tableData.push({
                    country: 'New Country',
                    name: 'New Name',
                    isActive: 'Yes',
                });
                this.tableData.push({
                    country: 'New Country',
                    name: 'New Name',
                    isActive: 'Yes',
                });
            } else {
                this.tableData = []
                this.counter = 0
            }
            this.counter = this.counter + 1
        }, 1000);
    },

    beforeUnmount() {
        clearInterval(this.intervalId);
    },
}
</script>

<style></style>