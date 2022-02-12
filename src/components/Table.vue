<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
    title: string,
    desc: string,
    header: Array<string>,
    columns: Array<Array<string>>,
}>();

const rows = computed(() => {
    let rows: string[][] = [];

    if (props.columns.length == 0) {
        return [[]];
    }

    for (let r = 0; r < props.columns[0].length; r++) {
        let row: string[] = [];
        for (let c = 0; c < props.columns.length; c++) {
            row.push(props.columns[c][r]);
        }
        rows.push(row);
    }

    return rows;
});

</script>

<template>
    <div class="flex flex-col items-center border-collapse text-center">
        <table class="table-auto text-sm">
            <thead>
                <tr>
                    <th
                        v-for="col in header"
                        class="border-b dark:border-slate-600 font-medium text-slate-400 dark:text-slate-200 border"
                        v-html="col"
                    ></th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="row in rows">
                    <td
                        v-for="col in row"
                        class="border-b border-slate-100 dark:border-slate-700 text-slate-500 dark:text-slate-400 p-1 border"
                    >
                        <span v-html="col"></span>
                    </td>
                </tr>
            </tbody>
        </table>
        <h2>{{ title }}</h2>
        <p class="text-sm text-gray-500">{{ desc }}</p>
    </div>
</template>>