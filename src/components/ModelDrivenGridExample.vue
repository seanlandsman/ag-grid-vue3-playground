<template lang="html">
    <div style="display: inline-block; width: 1100px">
        <h1>Model Driven Grid Example</h1>
        <h3>Note that the data bound table will not update as the row data is frozen.</h3>
        <div style="float: left; display: inline-grid">
            <span>Model Driven</span>
            <ag-grid-vue
                ref="model"
                class="ag-theme-alpine"
                style="width: 700px; height: 400px;"
                :modules="modules"
                :columnDefs="columnDefs"
                v-model="modelRowData"
                v-on:update:modelValue="modelChanges">
            </ag-grid-vue>
            <span>{{ modelRowData }}</span>
            <button @click="printRowData('modelRowData')">Print Row Data</button>
        </div>
    </div>
</template>
<script>
import {AgGridVue} from "@ag-grid-community/vue3";
import {ClientSideRowModelModule} from "@ag-grid-community/client-side-row-model";

export default {
    name: 'ModelDrivenGridExample',
    data() {
        return {
            columnDefs: null,
            modelRowData: null,
            modules: [ClientSideRowModelModule]
        };
    },
    beforeMount() {
        this.columnDefs = [
            {headerName: 'Make', field: 'make', editable: true},
            {headerName: 'Model', field: 'model', editable: true},
        ];

        const tempRowData = [
            {make: 'Toyota', model: 'Celica'}
        ];

        this.modelRowData = Object.freeze(
            this.copyRowData(tempRowData)
        );
    },
    methods: {
        modelChanges(updatedModel) {
            this.modelRowData = Object.freeze(
                this.copyRowData(updatedModel)
            );
        },
        printRowData(field) {
            this[field].forEach(datum => console.log(datum))
        },
        copyRowData(data) {
            return data.map(datum => {
                return {
                    ...datum
                }
            })
        }
    },
    components: {
        AgGridVue
    }
};
</script>
<style lang="css">
@import "~@ag-grid-community/core/dist/styles/ag-grid.css";
@import "~@ag-grid-community/core/dist/styles/ag-theme-alpine.css";
</style>

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
