<template>
  <div v-for="item in data" :key="item[idKey]">
    <label>
      <input
        type="checkbox"
        :checked="isChecked(item[idKey])"
        @change="toggleCheckbox(item[idKey])"
      />
      {{ item[labelKey] }}
    </label>
    <div :style="childrenStyle">
      <Tree
        v-if="item[childrenKey] && isChecked(item[idKey])"
        v-bind="props"
        :data="item[childrenKey]"
        v-model:selectedItems="selectedItems"
      />
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from "vue";

const props = defineProps({
  data: { type: Array },
  persist: { type: Boolean, default: true },
  idKey: { type: String, default: "id" },
  labelKey: { type: String, default: "label" },
  childrenKey: { type: String, default: "children" },
  storageKey: { type: String, default: "tree" },
  childrenStyle: { type: Object, default: { marginLeft: "1rem" } },
});

const selectedItems = defineModel("selectedItems", { default: () => [] });

const isChecked = (id) => selectedItems.value.includes(id);

const toggleCheckbox = (id) => {
  selectedItems.value = get();
  if (!isChecked(id)) {
    selectedItems.value = saveId(id);
  } else {
    selectedItems.value = removeId(id);
  }
};

/**
 * Method to initialize the storage and get the saved data from storage
 */
const get = () => {
  let tree = [];
  if (localStorage[props.storageKey]) {
    tree = JSON.parse(localStorage[props.storageKey]) ?? [];
  } else {
    localStorage[props.storageKey] = JSON.stringify(tree);
  }
  return tree;
};

/**
 *
 * @param {*} id  - props.idKey to save in storage
 */
const saveId = (id) => {
  let tree = get();
  tree.push(id);
  localStorage[props.storageKey] = JSON.stringify(tree);
  return tree;
};

/**
 *
 * @param {*} id - props.idKey to remove from storage
 */
const removeId = (id) => {
  let tree = get();
  tree = tree.filter((x) => x !== id);
  localStorage[props.storageKey] = JSON.stringify(tree);
  return tree;
};

onMounted(() => {
  // get stored id's
  selectedItems.value = get();
});

onUnmounted(() => {
  // remove all immediate children id's
  if (props.data && props.data.length) {
    props.data.forEach((item) => {
      removeId(item.id);
    });
  }
  selectedItems.value = get();
});
</script>
