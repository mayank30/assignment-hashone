# Hashone Coding Assignment

## Usage

```
  <Tree :data="data" v-model:selectedItems="selectedItems" />
```

## Props

| Props         | Type    | Default Value        | Description                                                                           |
| ------------- | ------- | -------------------- | ------------------------------------------------------------------------------------- |
| data          | Array   | []                   | Data to render                                                                        |
| persist       | Boolean | true                 | Selection to persist in LocalStorage                                                  |
| idKey         | String  | id                   | any unique attribute key can be as idKey                                              |
| labelKey      | String  | "label"              | any field to display from data to be pass to render                                   |
| childrenKey   | String  | "children"           | any children prop can be pass from your data array to pick                            |
| storageKey    | String  | "tree"               | if you want to save selected in storage with any other key name can be configure here |
| childrenStyle | Object  | {marginLeft: "1rem"} | style the children currently margin left can be configured                            |

## Events

| Event         | Return | Description                             |
| ------------- | ------ | --------------------------------------- |
| selectedItems | Array  | Whatever id's were checked are returned |

### Advance Usage

```
<Tree
    :data="data"
    v-model:selectedItems="selectedItems"
    storageKey="tree-view"
    idKey="uniqueId"
    childrenKey="child"
    labelKey="text"
  />

// For eg below data
data = [ {
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
      }]
}]
```

### Example Data Object

```
const data = [
  {
    id: 1,
    label: "Parent 1",
    children: [
      {
        id: 2,
        label: "Child 1.1",
        children: [
          { id: 4, label: "Child 1.1.1" },
          { id: 5, label: "Child 1.1.2" },
        ],
      },
      {
        id: 3,
        label: "Child 1.2",
        children: [{ id: 6, label: "Child 1.2.1" }],
      },
    ],
  },
  {
    id: 7,
    label: "Parent 2",
    children: [
      { id: 8, label: "Child 2.1" },
      {
        id: 9,
        label: "Child 2.2",
        children: [
          {
            id: 10,
            label: "Child 2.2.1",
            children: [
              { id: 11, label: "Child 2.2.1.1" },
              { id: 12, label: "Child 2.2.1.2" },
            ],
          },
        ],
      },
    ],
  },
]
```
