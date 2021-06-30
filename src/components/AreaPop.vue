<template>
  <div class="area-pop">
    <template v-for="item in treeData">
      <a-checkbox
        :key="item.key"
        :indeterminate="item.indeterminate"
        :checked="item.checkAll"
        :value="item.key"
        @change="onCheckAllChange"
      >
        <template v-if="!item.children">{{ item.title }}</template>
        <a-popover v-else placement="right" trigger="click" :key="item.key">
          <div slot="content" @click="onClick(item)">
            <a-checkbox-group
              class="check-box-group"
              :options="item.children"
              v-model="item.checkedList"
              @change="onChange"
            >
              <span slot="label" slot-scope="scope" style="color: red">
                <a-popover
                  placement="right"
                  trigger="click"
                  @click="onClick(scope, item)"
                >
                  <template slot="content">
                    <AreaPop
                      class="inner-area-item"
                      :treeData="scope.children"
                    ></AreaPop>
                  </template>
                  {{ scope.title }}
                </a-popover>
              </span>
            </a-checkbox-group>
          </div>
          {{ item.title }}
        </a-popover>
      </a-checkbox>
    </template>
  </div>
</template>

<script>
const plainOptions = ["Apple", "Pear", "Orange"];
export default {
  name: "AreaPop",
  props: {
    treeData: [],
  },
  data() {
    return {
      checkedList: [],
      indeterminate: true,
      checkAll: false,
      plainOptions,
    };
  },
  methods: {
    onClick(item, pItem) {
      this.curItem = item || {};
      this.curPItem = pItem || {};
      console.log(this.curItem, this.curPItem);
    },
    onChange(checkedList) {
      console.log(checkedList);
      // this.curPItem.indeterminate =
      //   !!checkedList.length &&
      //   checkedList.length < this.curItem.children.length;
      // if (this.curPItem.value) {
      //   console.log(this.curPItem);
      // } else {
      //   this.curItem.checkAll =
      //     checkedList.length === this.curItem.children.length;
      // }
      // this.curItem.indeterminate = this.curPItem.indeterminate;
      // this.curItem.checkAll = this.curPItem.checkAll;
      console.log(this.curPItem, this.curItem);
    },
    onChangeChild(value) {
      console.log("ppp", value);
    },
    onCheckAllChange(e) {
      if (e.target) {
        let tree = this.changeTree(this.treeData, e.target.value);
        if(tree.children) {
          Object.assign(tree, {
            checkedList: e.target.checked
              ? this.getAllNodeId([], tree.children)
              : [],
            indeterminate: false,
            checkAll: e.target.checked,
          });
        }
      }
    },
    changeTree(list, key) {
      for (let index = 0; index < list.length; index++) {
        const item = list[index];
        if (item.key == key) {
          return item;
        } else {
          item.children && this.changeTree(item.children, key);
        }
      }
    },
    getAllNodeId(keys, tree) {
      for (let i = 0; i < tree.length; i++) {
        keys.push(tree[i].value);
        if (tree[i].children) {
          this.$set(tree[i], "checkedList", [])
          keys = this.getAllNodeId(keys, tree[i].children);
        }
      }
      return keys;
    },
    allCkecked(list) {
      for (let index = 0; index < list.length; index++) {
        const item = list[index];
        if (item.children) {
          item.children && this.allCkecked(item.children);
        }
      }
    },
  },
  created() {
    this.getAllNodeId([], this.treeData)
  }
};
</script>

<style lang="less" scoped>
.check-box-group {
  min-width: 100px;
  /deep/ .ant-checkbox-group-item {
    display: block;
  }
}
.area-pop {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  .check-box-group {
    width: 300px;
  }
  .ant-checkbox-wrapper {
    width: 33.333%;
    margin-left: 0 !important;
    margin-bottom: 10px;
  }
}
.inner-area-item {
  display: block;
  > .ant-checkbox-wrapper {
    display: block;
    width: 100%;
  }
}
.area-content {
  max-width: 200px;
  max-height: 400px;
  overflow: hidden;
  .area-pop {
    display: block;
  }
  .ant-checkbox-wrapper {
    display: block;
    margin-left: 0 !important;
  }
}
</style>
