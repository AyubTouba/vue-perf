<template >
    <tr v-if="item.isShowen">
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
</template>

<script>
export default {

    props: ["item"],
    watch: {
        item: function (newVal, oldVal) { // watch it
            console.log('Id', this.item.id, 'Prop changed: ', newVal, ' | was: ', oldVal)
        }
    }
}
</script>

<style></style>