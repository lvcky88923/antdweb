<template>
  <div class="area-list">
    <div v-for="item in treeData" :key="item.key">
      <a-checkbox
        :indeterminate="indeterminate"
        :checked="checkAll"
        @change="onCheckAllChange"
        >{{ item.title }}</a-checkbox
      >
      <AreaPop :treeData="item.children"></AreaPop>
    </div>
  </div>
</template>

<script>
const plainOptions = ["Apple", "Pear", "Orange"];
const defaultCheckedList = ["Apple", "Orange"];
import AreaPop from "./AreaPop";
export default {
  name: "AreaList",
  components: {
    AreaPop,
  },
  props: {
    treeData: [],
  },
  data() {
    return {
      checkedList: defaultCheckedList,
      indeterminate: true,
      checkAll: false,
      plainOptions,
    };
  },
  methods: {
    onChange(checkedList) {
      this.indeterminate =
        !!checkedList.length && checkedList.length < plainOptions.length;
      this.checkAll = checkedList.length === plainOptions.length;
    },
    onCheckAllChange(e) {
      Object.assign(this, {
        checkedList: e.target.checked ? plainOptions : [],
        indeterminate: false,
        checkAll: e.target.checked,
      });
    },
  },
};
</script>

<style lang="less" scoped>
.area-list {
  > div {
    display: flex;
    > label {
      flex: none;
    }
  }
  .area-pop {
    margin-left: 30px;
  }
}
</style>
