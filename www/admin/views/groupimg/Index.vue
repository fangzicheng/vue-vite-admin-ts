<template>
    <bag-curd-table :createForm="createForm" :editForm="editForm" :tableCurd="tableCurd"></bag-curd-table>
</template>
<script lang="ts">
import { defineComponent, reactive } from 'vue'
import { cloneDeep } from 'lodash'
import curdTableHock, { initTableHock } from '@/packages/hook/table'
import columns from './columns'

export default defineComponent({
    setup() {
        const { tableCurd } = curdTableHock()
        const form = reactive(initTableHock({
            columns, tableCurd, options: {
                apiPrefix: '/web/groupimg',
            },
        }))
        return {
            tableCurd,
            editForm: { ...form },
            createForm: { ...cloneDeep(form) },
        }
    },
})
</script>
