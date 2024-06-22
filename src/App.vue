<template>
  <h2>Tree view</h2>
  <Tree
    :data="data"
    v-model:selectedItems="selectedItems"
    storageKey="tree-view"
    idKey="uniqueId"
    childrenKey="child"
    labelKey="text"
  />

  <div v-if="selectedItems.length">
    <h4>Selected Items</h4>
    {{ selectedItems }} &nbsp;
    <a @click="onReset">Reset</a>
  </div>
</template>
<script setup>
import { ref } from "vue";
import Tree from "./components/Tree.vue";
const data = [
  {
    uniqueId: 1,
    text: "Parent 1",
    child: [
      {
        uniqueId: 2,
        text: "Child 1.1",
        child: [
          { uniqueId: 4, text: "Child 1.1.1" },
          { uniqueId: 5, text: "Child 1.1.2" },
        ],
      },
      {
        uniqueId: 3,
        text: "Child 1.2",
        child: [{ uniqueId: 6, text: "Child 1.2.1" }],
      },
    ],
  },
  {
    uniqueId: 7,
    text: "Parent 2",
    child: [
      { uniqueId: 8, text: "Child 2.1" },
      {
        uniqueId: 9,
        text: "Child 2.2",
        child: [
          {
            uniqueId: 10,
            text: "Child 2.2.1",
            child: [
              { uniqueId: 11, text: "Child 2.2.1.1" },
              { uniqueId: 12, text: "Child 2.2.1.2" },
            ],
          },
        ],
      },
    ],
  },
];
const selectedItems = ref([]);
const onReset = () => {
  localStorage.clear();
  selectedItems.value = [];
};
</script>