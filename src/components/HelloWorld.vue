<script setup lang="ts">
import { ref } from 'vue'
import Table from './Table.vue'

const domain = ref([["1", "w", "w<sup>2</sup>", "w<sup>3</sup>"]]);

function create_table(cols: number, rows: number): string[][] {
  let table: string[][] = [];
  for (let r = 0; r < cols; r++) {
    let row: string[] = [];
    for (let c = 0; c < rows; c++) {
      row.push("x");
    }
    table.push(row);
  }
  return table;
}

</script>

<template>
  <div class="container mx-auto h-screen pt-10 pb-10">
    <h1>Kimchi: A visualization</h1>
    <div class="flex flex-row gap-5 h-full pt-10 pb-10">
      <!-- domain -->
      <div class="basis-1/12 h-full">
        <h2 class="text-center">Domain</h2>
        <div class="flex flex-row border p-2 h-full">
          <Table title="domain" desc="the domain" :header="['/']" :columns="domain" />
        </div>
      </div>
      <!-- circuit spec -->
      <div class="basis-5/12 h-full">
        <h2 class="text-center">Circuit spec</h2>
        <div class="flex flex-row border p-2 h-full">
          <Table
            title="coeffs"
            desc="used to tweak some gates like poseidon or the generic gate"
            :header="[...Array(15)].map((_, i) => i.toString())"
            :columns="create_table(15, 4)"
          />
          <Table
            title="gates"
            desc="the gate selectors that enforce which gate is being used in a specific row"
            :header="['generic', 'poseidon', '...']"
            :columns="[['1', '0', '1', '0'], ['0', '1', '0', '0'], ['', '', '', '']]"
          />
          <Table
            title="sigmas"
            desc="each IO register is assigned to a sigma, which tells us what other IO register it is wired to"
            :header="[...Array(7)].map((_, i) => i.toString())"
            :columns="create_table(7, 4)"
          />
        </div>
      </div>
      <!-- execution trace -->
      <div class="basis-5/12 h-full">
        <h2 class="text-center">Execution trace</h2>
        <div class="flex flex-row border p-2 h-full">
          <Table
            title="IO registers"
            desc="also called witness columns or wires. IO registers can be wired"
            :header="[...Array(7)].map((_, i) => i.toString())"
            :columns="create_table(7, 4)"
          />
          <Table
            title="advice registers"
            desc="advice registers can hold values needed by a gate's constraints"
            :header="[...Array(8)].map((_, i) => i.toString())"
            :columns="create_table(8, 4)"
          />
          <Table
            title="permutation"
            desc="holds the permutation values"
            :header="[...Array(7)].map((_, i) => i.toString())"
            :columns="create_table(7, 4)"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>
