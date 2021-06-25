<template>
  <a-table
    ref="table"
    :row-selection="rowSelection"
    :columns="columns"
    rowKey="id"
    :data-source="data"
  >
    <!-- <a slot="name" slot-scope="text">{{ text }}</a> -->
  </a-table>
</template>

<script>
const columns = [
  {
    title: "Name",
    dataIndex: "name",
    scopedSlots: { customRender: "name" },
  },
  {
    title: "Age",
    dataIndex: "age",
  },
  {
    title: "Address",
    dataIndex: "address",
  },
];
const data = [
  {
    id: 1,
    key: 1,
    name: "John Brown",
    age: 32,
    disabled: false,
    address: "New York No. 1 Lake Park",
  },
  {
    id: 2,
    key: 2,
    name: "Jim Green",
    age: 42,
    disabled: false,
    address: "London No. 1 Lake Park",
  },
  {
    id: 3,
    key: 3,
    name: "Joe Black",
    disabled: false,
    age: 32,
    address: "Sidney No. 1 Lake Park",
  },
  {
    id: 4,
    key: 4,
    name: "Disabled User",
    age: 99,
    disabled: false,
    address: "Sidney No. 1 Lake Park",
  },
];
export default {
  data() {
    return {
      data,
      columns,
      defaultKeys: [1, 2],
    };
  },
  computed: {
    rowSelection() {
      return {
        columnTitle: "选择", // 去掉头部全选框
        hideDefaultSelections: true,
        onChange: (selectedRowKeys, selectedRows) => {
          // 去重
          selectedRowKeys = Array.from(new Set(selectedRowKeys)).slice(0, 2);
          selectedRows = selectedRows.filter(
            (item) => selectedRowKeys.indexOf(item.key) !== -1
          );
          console.log(selectedRows);
          this.defaultKeys = [...selectedRowKeys];
          this.onChangeTable(this.defaultKeys);
        },
        getCheckboxProps: (record) => {
          let disabled = record.disabled;
          return {
            props: {
              defaultChecked: this.defaultKeys.includes(record.key),
              disabled,
            },
          };
        },
      };
    },
  },
  mounted() {
    this.onChangeTable(this.defaultKeys);
  },
  methods: {
    onChangeTable(rowKeys) {
      for (let index = 0; index < this.data.length; index++) {
        const item = this.data[index];
        if (rowKeys.indexOf(item.key) == -1 && rowKeys.length >= 2) {
          item.disabled = true;
        } else {
          item.disabled = false;
        }
      }
      // let disabled = rowKeys.length >= 2;
      // this.data.forEach(
      //   item => rowKeys.indexOf(item.key) === -1 && (item.disabled = disabled)
      // );
      // 重新赋值
      this.data = [...this.data];
    },
  },
};
</script>

<style></style>
