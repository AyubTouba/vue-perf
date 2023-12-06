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
                            <div class="sm:col-span-3">
                                <label for="af-submit-application-full-name"
                                    class="inline-block text-sm font-medium text-gray-500 mt-2.5">
                                    Id Item to Change
                                </label>
                            </div>
                            <div class="sm:col-span-9">
                                <div class="sm:flex">
                                    <input id="item" type="text" v-model="inputId"
                                        class="bg-blue-600 py-2 px-3 pe-11 block w-full border-gray-200 shadow-sm -mt-px -ms-px first:rounded-t-lg last:rounded-b-lg sm:first:rounded-s-lg sm:mt-0 sm:first:ms-0 sm:first:rounded-se-none sm:last:rounded-es-none sm:last:rounded-e-lg text-sm relative focus:z-10 focus:border-blue-500 focus:ring-blue-500 disabled:opacity-50 disabled:pointer-events-none dark:bg-slate-900 dark:border-gray-700 dark:text-gray-400 dark:focus:ring-gray-600">
                                </div>
                            </div>
                            <button type="button" @click="changeItem()"
                                class="py-3 px-4 inline-flex justify-center items-center gap-x-2 text-sm font-semibold rounded-lg border border-transparent bg-blue-600 text-white hover:bg-blue-700 disabled:opacity-50 disabled:pointer-events-none dark:focus:outline-none dark:focus:ring-1 dark:focus:ring-gray-600">
                                Submit
                            </button>
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
                                <ItemTable v-for="(item) in tableData" :key="item.id" :item="item" />
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
import ItemTable from './ItemTable.vue';

export default {
    data() {
        return {
            tableData: [],
            intervalId: null,
            counter: 0,
            inputId: null
        };
    },

    methods: {
        changeItem() {
            this.tableData = this.tableData.map(dt => dt.id == this.inputId ?
                { ...dt, name: this.generateRandomString(8), isShowen: !dt.isShowen } : dt)
        },
        generateRandomString(length) {
            const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
            let result = '';

            for (let i = 0; i < length; i++) {
                const randomIndex = Math.floor(Math.random() * characters.length);
                result += characters.charAt(randomIndex);
            }

            return result;
        }
    },
    mounted() {
        // Simulate a memory leak by creating a setInterval without clearing it
        this.intervalId = setInterval(() => {
            // Push new data to the tableData array
            if (this.counter <= 10) {
                this.tableData.push({
                    id: this.counter,
                    country: 'New Country',
                    name: 'New Name',
                    isActive: 'Yes',
                    isShowen: true
                });
            }
            else {
                this.tableData = this.tableData.filter(dt => ![9, 10, 8].includes(dt.id));
                this.counter = 8;
            }
            this.counter = this.counter + 1;
        }, 1000);
    },
    beforeUnmount() {
        clearInterval(this.intervalId);
    },
    components: { ItemTable }
}
</script>

<style></style>