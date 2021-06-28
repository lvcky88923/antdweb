<template>
  <div class="area-pop">
    <template v-for="item in treeData">
      <!-- <a-popover v-if="item.children" placement="right" trigger="click" :key="item.key">
        <template slot="content">
          <a-checkbox-group
            class="check-box-group"
            v-model="checkedList"
            :options="item.children"
            @change="onChange"
          >
            <span slot="label" slot-scope="{ title, children }" style="color: red">
              <a-popover placement="right" trigger="click">
                <template slot="content">
                  <AreaPop class="inner-area-item" :treeData="children"></AreaPop>
                </template>
                {{title}}
              </a-popover>
            </span>
          </a-checkbox-group>
        </template>
        <a-checkbox
          :indeterminate="indeterminate"
          :checked="checkAll"
          @change="onCheckAllChange"
        >{{item.title}}</a-checkbox>
      </a-popover>-->
      <a-checkbox
        v-if="item.children"
        :key="item.key"
        :indeterminate="indeterminate"
        :checked="checkAll"
        :value="item.key"
        @change="onCheckAllChange"
      >
        <a-popover v-if="item.children" placement="right" trigger="click" :key="item.key">
          <template slot="content">
            <a-checkbox-group class="check-box-group" :options="item.children">
              <span slot="label" slot-scope="{ title, children }" style="color: red">
                <a-popover placement="right" trigger="click">
                  <template slot="content">
                    <AreaPop class="inner-area-item" :treeData="children"></AreaPop>
                  </template>
                  {{ title }}
                </a-popover>
              </span>
            </a-checkbox-group>
          </template>
          {{ item.title }}
        </a-popover>
      </a-checkbox>
      <a-checkbox v-else :key="item.key" :value="item.key">
        {{
        item.title
        }}
      </a-checkbox>
    </template>
  </div>
</template>

<script>
const plainOptions = ["Apple", "Pear", "Orange"];
const defaultCheckedList = ["Apple", "Orange"];
export default {
  name: "AreaPop",
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
      console.log(this.changeTree(this.treeData, e.target.value))
      // for (let index = 0; index < this.treeData.length; index++) {
      //   const item = this.treeData[index];
      //   if(item.key == e.target.value) {
      //     console.log(item)
      //   } else {

      //   }
      // }
      console.log(e);
      if (e.target) {
        Object.assign(this, {
          checkedList: e.target.checked ? plainOptions : [],
          indeterminate: false,
          checkAll: e.target.checked,
        });
      }
    },
    changeTree(list, key) {
      for (let index = 0; index < list.length; index++) {
        const item = list[index];
        if(item.key == key) {
          console.log(item)
          return item
        } else {
          this.changeTree(item.children)
        }
      }
    },
  },
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
