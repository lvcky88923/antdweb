<template>
  <a-tree
    v-model="checkedKeys"
    checkable
    :expanded-keys="expandedKeys"
    :auto-expand-parent="autoExpandParent"
    :selected-keys="selectedKeys"
    :tree-data="treeData"
    @expand="onExpand"
    @check="onCheck"
    @select="onSelect"
  />
</template>
<script>
const treeData = [
  {
    title: "0-0",
    key: "0-0",
    children: [
      {
        title: "0-0-0",
        key: "0-0-0",
        children: [
          { title: "0-0-0-0", key: "0-0-0-0" },
          { title: "0-0-0-1", key: "0-0-0-1" },
          { title: "0-0-0-2", key: "0-0-0-2" },
        ],
      },
      {
        title: "0-0-1",
        key: "0-0-1",
        children: [
          { title: "0-0-1-0", key: "0-0-1-0" },
          { title: "0-0-1-1", key: "0-0-1-1" },
          { title: "0-0-1-2", key: "0-0-1-2" },
        ],
      },
      {
        title: "0-0-2",
        key: "0-0-2",
      },
    ],
  },
  //   {
  //     title: "0-1",
  //     key: "0-1",
  //     children: [
  //       { title: "0-1-0-0", key: "0-1-0-0" },
  //       { title: "0-1-0-1", key: "0-1-0-1" },
  //       { title: "0-1-0-2", key: "0-1-0-2" }
  //     ]
  //   },
  //   {
  //     title: "0-2",
  //     key: "0-2"
  //   }
];

export default {
  data() {
    return {
      expandedKeys: ["0-0-0", "0-0-1"],
      autoExpandParent: true,
      checkedKeys: ["0-0-0"],
      selectedKeys: [],
      treeData,
    };
  },
  //   watch: {
  //     checkedKeys(val) {
  //       console.log("onCheck", val);
  //     }
  //   },
  methods: {
    onExpand(expandedKeys) {
      console.log("onExpand", expandedKeys);
      // if not set autoExpandParent to false, if children expanded, parent can not collapse.
      // or, you can remove all expanded children keys.
      this.expandedKeys = expandedKeys;
      this.autoExpandParent = false;
    },
    onCheck(checkedKeys, e) {
      console.log("onCheck", checkedKeys);
      console.log("info", e);
      this.checkedKeys = checkedKeys;
    },
    onSelect(selectedKeys, info) {
      console.log("onSelect", info);
      this.selectedKeys = selectedKeys;
    },
  },
};
</script>

<style>
.ant-tree > li {
  display: flex;
}
.ant-tree li {
  padding: 0 !important;
}
.ant-tree-child-tree > li:first-child {
  padding: 0 !important;
}
.ant-tree > li > .ant-tree-child-tree {
  flex: 1;
  display: flex;
  padding: 0 0 0 40px;
}
.ant-tree-child-tree li {
  padding-top: 0;
  width: 10%;
}
</style>
